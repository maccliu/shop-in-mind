# bc_stu 基本表

商品主表。

## SQL定义

```sql
DROP TABLE IF EXISTS `bc_stu`;

CREATE TABLE `bc_stu` (
  `stu_id` int(11) NOT NULL AUTO_INCREMENT,

  `warehouse_id` tinyint(4) NOT NULL COMMENT '发货仓id',

  `title` varchar(255) NOT NULL COMMENT '商品标题',

  `weight` float DEFAULT NULL COMMENT '商品重量',
  `weight_unit` varchar(16) DEFAULT '克' COMMENT '重量单位',

  `on_sale` tinyint(1) NOT NULL DEFAULT '0' COMMENT '上架：1上架 0下架',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '已删除',

  `image` varchar(255) DEFAULT NULL COMMENT '主图',
  `thumb` varchar(255) DEFAULT NULL COMMENT '缩略图',

  `brand_id` int(11) NOT NULL DEFAULT '0' COMMENT '品牌id',

  `uom` varchar(20) DEFAULT NULL COMMENT '销售单位',

  `attrs` blob COMMENT '单品参数 json格式',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`stu_id`),
  KEY `brand_id` (`brand_id`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品表';

```

> 备注
> 1. 为考虑尽可能兼容原系统中的商品数据，所以本表中的`stu_id`**没有设计成自增**，必须明确指定。
> 2. `stu_id`的1-9999 保留给原系统的商品新西兰仓使用，10000-19999 保留给原系统商品的国内仓使用，新系统的商品用100000（6位数）id，以免和原系统商品冲突。
> 3. 为确保数据一致性，1-9999 和 10001-19999 是严格的一一对应关系。


## 从原ECSHOP中导入商品数据

```sql

/* 删除旧数据 */
DELETE FROM
  `bc_stu`
WHERE
  `stu_id` BETWEEN 1 AND 19999;


/* 商品，新西兰直邮仓 */
INSERT INTO
  `bc_stu`
    (
    `stu_id`,
    `warehouse_id`,
    `title`,
    `weight`,
    `weight_unit`,
    `on_sale`,
    `deleted`,
    `image`,
    `thumb`,
    `brand_id`,
    `created_at`,
    `updated_at`
    )

  SELECT
    `goods_id`,
    2,
    `goods_name`,
    `goods_weight` * 1000,
    '克',
    `is_on_sale`,
    `is_delete`,
    `goods_img`,
    `goods_thumb`,
    `brand_id`,
    from_unixtime(`add_time`),
    from_unixtime(`last_update`)
  FROM
    `cn_goods`
;


/* 商品，国内仓 */
INSERT INTO
  `bc_stu`
    (
    `stu_id`,
    `warehouse_id`,
    `title`,
    `weight`,
    `weight_unit`,
    `on_sale`,
    `deleted`,
    `image`,
    `thumb`,
    `brand_id`,
    `created_at`,
    `updated_at`
    )

  SELECT
    (`goods_id` + 10000),
    1,
    `goods_name`,
    `goods_weight` * 1000,
    '克',
    `is_on_sale`,
    `is_delete`,
    `goods_img`,
    `goods_thumb`,
    `brand_id`,
    from_unixtime(`add_time`),
    from_unixtime(`last_update`)
  FROM
    `cn_goods`
;

```
