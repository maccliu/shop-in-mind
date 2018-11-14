# bc_stu_price 基本表

商品价格池。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_stu_price`;

CREATE TABLE `bc_stu_price` (
  `price_id` int(11) NOT NULL AUTO_INCREMENT,
  `stu_id` int(11) NOT NULL COMMENT '商品SPU#',

  `user_rank` tinyint(4) NOT NULL DEFAULT '0' COMMENT '适用的用户级别(0为适用所有级别)',

  `price_level` tinyint(4) NOT NULL COMMENT '价格级别：10日常价 20仓库价 30促销价 40节日价',
  `currency` varchar(3) DEFAULT 'NZD' COMMENT '基准币种',
  `price` decimal(12,2) NOT NULL COMMENT '价格',
  `start_at` datetime DEFAULT NULL COMMENT '价格的开始时间',
  `end_at` datetime DEFAULT NULL COMMENT '价格的截止时间',
  `free_shipping` tinyint(4) NOT NULL DEFAULT '0' COMMENT '是否包邮 1包邮 0不包邮',
  `price_tag` varchar(255) DEFAULT NULL COMMENT '价格标签',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  `updated_by` int(11) DEFAULT NULL COMMENT '更新人',

  PRIMARY KEY (`price_id`),
  UNIQUE KEY `uni_key` (`stu_id`,`user_rank`,`price_level`,`currency`,`price`,`start_at`,`end_at`,`free_shipping`),
  KEY `stu_id` (`stu_id`),
  KEY `user_rank` (`user_rank`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品价格表';

```

> 备注:
> 1. 价格根据 `price_level` 进行了分层，高层价格会覆盖底层价格。满足(stu_id, user_rank, time) 条件的最高`price_level`的价格即为实际价格。
> 2. 原则上，同一个商品，高层价格<=底层价格，不然容易被客户质疑“怎么促销价/活动价还比日常价高”。但是考虑到定价属于商家经营策略范畴，有很大主观性，除非商家本身要求，否则程序不应该介入。所以，程序不会强制使用较低价格作为实际价格。
> 3. `price_tag` 可以设置价格标签，比如说“店庆”，“情人节特价”等。
> 4. 价格的所有字段都会在订单商品表中会被标记出来。


## 从ECSHOP中导入数据

```sql

/*
  清空价格表，根据需要看是不是重置整个价格池
  如果员工已经设置了一些商品的价格，则不要用这条语句。
*/
TRUNCATE TABLE `bc_stu_price`;


/*
  只删除 ECSHOP 导入的商品价格（id<20000,且价格级别为10，20，30的记录）
*/
DELETE FROM
  `bc_stu_price`
WHERE
  `stu_id` < 20000
  AND `price_level` IN (10, 20, 30)
;


/*
  导入 cn_goods 中的会员基本价格
  币种为NZD
*/
INSERT INTO
  `bc_stu_price`
    (
    `stu_id`,
    `user_rank`,
    `price_level`,
    `currency`,
    `price`,
    `free_shipping`,
    `updated_at`
    )

  SELECT
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`,
    10 AS `price_level`,
    'NZD' AS `currency`,
    round(`cn_goods`.`shop_price` * `cn_user_rank`.`discount` / 100.0, 2) AS `price`,
    `cn_goods`.`is_shipping`,
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods`,
    `cn_user_rank`
  WHERE
    `cn_goods`.`shop_price` > 0
  ORDER BY
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`

ON DUPLICATE KEY UPDATE
  `stu_id` = `stu_id`
;


/*
  导入 cn_goods_ex 的新西兰仓价格
  注意：bc_goods_ex表中的币种字段不正确，不管currency字段是NZD还是RMB，都应为NZD。
*/
INSERT INTO
  `bc_stu_price`
    (
    `stu_id`,
    `user_rank`,
    `price_level`,
    `currency`,
    `price`,
    `free_shipping`,
    `updated_at`
    )

  SELECT
    `cn_goods_ex`.`goods_id`,
    `cn_user_rank`.`rank_id`,
    20 AS `price_level`,
    "NZD",
    round(`cn_goods_ex`.`price` * `cn_user_rank`.`discount` / 100.0, 2) AS `price`,
    `cn_goods`.`is_shipping`,
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods_ex`
  LEFT JOIN
    `cn_user_rank`
      ON true
  INNER JOIN
    `cn_goods`
      ON
        `cn_goods_ex`.`goods_id` = `cn_goods`.`goods_id`
  WHERE
    `cn_goods_ex`.`warehouse_id` = 2
    AND `cn_goods_ex`.`price` IS NOT NULL
    AND `cn_goods_ex`.`price` > 0
  ORDER BY
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`

ON DUPLICATE KEY UPDATE
  `stu_id` = `stu_id`
;


/*
  导入 cn_goods_ex 的国内仓价格
  注意：bc_goods_ex表中的币种字段不正确，不管currency字段是NZD还是RMB，都应为NZD。
  注意：stu_id是(goods_id + 10000)
*/
INSERT INTO
  `bc_stu_price`
    (
    `stu_id`,
    `user_rank`,
    `price_level`,
    `currency`,
    `price`,
    `free_shipping`,
    `updated_at`
    )

  SELECT
    (`cn_goods_ex`.`goods_id` + 10000),
    `cn_user_rank`.`rank_id`,
    20 AS `price_level`,
    "NZD",
    round(`cn_goods_ex`.`price` * `cn_user_rank`.`discount` / 100.0, 2) AS `price`,
    `cn_goods`.`is_shipping`,
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods_ex`
  LEFT JOIN
    `cn_user_rank`
      ON true
  INNER JOIN
    `cn_goods`
      ON
        `cn_goods_ex`.`goods_id` = `cn_goods`.`goods_id`
  WHERE
    `cn_goods_ex`.`warehouse_id` = 1
    AND `cn_goods_ex`.`price` IS NOT NULL
    AND `cn_goods_ex`.`price` > 0
  ORDER BY
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`

ON DUPLICATE KEY UPDATE
  `stu_id` = `stu_id`
;


/*
  导入 cn_goods 里面的促销价
  此促销价仅针对新西兰仓商品
  币种为NZD
*/
INSERT INTO
  `bc_stu_price`
    (
    `stu_id`,
    `user_rank`,
    `price_level`,
    `currency`,
    `price`,
    `start_at`,
    `end_at`,
    `free_shipping`,
    `price_tag`,
    `updated_at`
    )

  SELECT
    `cn_goods`.`goods_id`,
    `cn_user_rank`.`rank_id`,
    30 AS `price_level`,
    'NZD' AS `currency`,
    `cn_goods`.`promote_price`,

    CASE
        WHEN
          `promote_start_date` > 0
        THEN
          FROM_UNIXTIME(`cn_goods`.`promote_start_date`)
        ELSE
          NULL
    END AS `start_at`,

    CASE
        WHEN
          `promote_end_date` > 0
        THEN
          FROM_UNIXTIME(`cn_goods`.`promote_end_date`)
        ELSE
          NULL
    END AS `end_at`,

    `cn_goods`.`is_shipping`,
    '促销',
    from_unixtime(`cn_goods`.`last_update`) AS `updated_at`
  FROM
    `cn_goods`
  LEFT JOIN
    `cn_user_rank`
      ON true
  WHERE
    `cn_goods`.`promote_price` > 0
  ORDER BY
    `cn_goods`.`goods_id`

ON DUPLICATE KEY UPDATE
  `stu_id` = `stu_id`
;

```
