# bc_spu_price 基本表

商品价格表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_spu_price`;

CREATE TABLE `bc_spu_price` (
  `id_price` int(11) NOT NULL AUTO_INCREMENT,

  `id_spu` int(11) NOT NULL COMMENT '商品SPU#',
  `id_warehouse` tinyint(4) NOT NULL COMMENT '仓库#(0为适用所有仓库)',
  `user_rank` tinyint(4) NOT NULL DEFAULT '0' COMMENT '适用的用户级别(0为适用所有级别)',
  
  `price_type` tinyint(4) NOT NULL COMMENT '价格类型：10日常价 20仓库价 30促销价 40节日价',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '基准币种',
  `price` decimal(12,2) NOT NULL COMMENT '价格',

  `start_at` datetime DEFAULT NULL COMMENT '价格的开始时间',
  `end_at` datetime DEFAULT NULL COMMENT '价格的截止时间',

  `post_free` tinyint(4) NOT NULL DEFAULT '0' COMMENT '免邮 1免邮 0不免邮',
  
  `price_tag` varchar(255) COMMENT '价格标签',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  `updated_by` int(11) DEFAULT NULL COMMENT '更新人',

  PRIMARY KEY (`id`),
  UNIQUE KEY `uni_key` (`id_spu`,`id_warehouse`,`user_rank`,`price_type`,`currency`,`price`,`start_at`,`end_at`,`post_free`),
  KEY `id_spu` (`id_spu`),
  KEY `id_warehouse` (`id_warehouse`),
  KEY `user_rank` (`user_rank`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品价格表';

```

> 备注:
> 1. 价格根据`price_type`进行了分层，高层价格会覆盖底层价格。满足(id_spu, id_warehouse, user_rank, time)条件的最高层的价格即为实际价格。
> 2. 原则上，同一个商品，高层价格<=底层价格，不然容易被客户质疑“怎么促销价/活动价还比日常价高”。但是考虑到定价属于商家经营策略范畴，有很大主观性，除非商家本身要求，否则程序不应该介入。所以，程序不会强制使用较低价格作为实际价格。
> 3. `price_tag` 可以设置价格标签，比如说“店庆”，“情人节特价”等。
> 4. 价格的所有字段都会在订单商品表中会被标记出来。


## 从ECSHOP中导入数据

```sql

/* 清空价格表 */
TRUNCATE TABLE `bc_spu_price`;


/* 导入 cn_goods 中的会员基本价格 */
INSERT INTO
  `bc_spu_price`
    (
    `id_spu`,
    `id_warehouse`,
    `user_rank`,
    `price_type`,
    `currency`,
    `price`,
    `post_free`,
    `updated_at`
    )

  SELECT
    `cn_goods`.`goods_id`,
    2 AS `warehouse`,
    `cn_user_rank`.`rank_id`,
    10 AS `price_type`,
    'NZD' AS `currency`,
    round(`cn_goods`.`shop_price` * `cn_user_rank`.`discount` / 100.0, 2) AS `price`,
    `cn_goods`.`is_shipping`,
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods`,
    `cn_user_rank`
  ORDER BY
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`

ON DUPLICATE KEY UPDATE
   `id_spu` = `id_spu`
;


/* 导入 cn_goods_ex 的仓库价 */
INSERT INTO
  `bc_spu_price`
    (
    `id_spu`,
    `id_warehouse`,
    `user_rank`,
    `price_type`,
    `currency`,
    `price`,
    `post_free`,
    `updated_at`
    )

  SELECT
    `cn_goods_ex`.`goods_id`,
    `cn_goods_ex`.`warehouse_id`,
    `cn_user_rank`.`rank_id`,
    20 AS `price_type`,
    'NZD' AS `currency`,
    round(`cn_goods`.`shop_price` * `cn_user_rank`.`discount` / 100.0, 2) AS `price`,
    `cn_goods`.`is_shipping`,
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods_ex`
  INNER JOIN
    `cn_goods`
      ON
        `cn_goods_ex`.`goods_id` = `cn_goods`.`goods_id`
  LEFT JOIN
    `cn_user_rank`
      ON true
  ORDER BY
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`

ON DUPLICATE KEY UPDATE
   `id_spu` = `id_spu`
;


/* 导入 cn_goods 的促销价 */
INSERT INTO
  `bc_spu_price`
    (
    `id_spu`,
    `id_warehouse`,
    `user_rank`,
    `price_type`,
    `currency`,
    `price`,
    `start_at`,
    `end_at`,
    `post_free`,
    `updated_at`
    )

  SELECT
    `cn_goods`.`goods_id`,
    0 AS `warehouse`,
    0 AS `user_rank`,
    30 AS `price_type`,
    'NZD' AS `currency`,
    `cn_goods`.`promote_price`,
    from_unixtime(`cn_goods`.`promote_start_date`) AS `start`,
    from_unixtime(`cn_goods`.`promote_end_date`) AS `end`,
    `cn_goods`.`is_shipping`,
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods`
  WHERE
    `cn_goods`.`promote_price` > 0
  ORDER BY
    `cn_goods`.`goods_id`

ON DUPLICATE KEY UPDATE
   `id_spu` = `id_spu`
;
```
