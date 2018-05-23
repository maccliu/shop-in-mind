# bc_spu 基本表

## SQL定义

```sql
DROP TABLE IF EXISTS `bc_spu`;

CREATE TABLE `bc_spu` (
  `id_spu` int(11) NOT NULL,
  `title` varchar(255) NOT NULL COMMENT '商品标题',
  `uom` varchar(20) DEFAULT NULL COMMENT '销售单位',
  `weight` float DEFAULT NULL COMMENT '商品重量',
  `weight_unit` varchar(16) DEFAULT '克' COMMENT '重量单位',
  `image` varchar(255) DEFAULT NULL COMMENT '主图',
  `thumb` varchar(255) DEFAULT NULL COMMENT '缩略图',
  `id_article` int(11) DEFAULT NULL COMMENT '商品文案#',
  `on_sale` tinyint(1) NOT NULL DEFAULT '0' COMMENT '上架：1上架 0下架',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '已删除',
  `attrs` blob COMMENT '商品参数 json格式',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id_spu`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品表';
```

> 备注
> 1. 为考虑尽可能兼容原系统中的商品数据，所以本表中的`id_spu`没有设计成自增，必须明确指定。
> 2. `id_spu`的1-9999 保留给原系统的商品数据使用。新的商品最好使用10000以上的id，以免和原系统商品冲突。


## 从原ECSHOP中导入商品数据

```sql
/* 从 cn_goods 中导入数据 */
INSERT INTO
  `bc_spu`
    (
    `id_spu`,
    `title`,
    `uom`,
    `weight`,
    `weight_unit`,
    `image`,
    `thumb`,
    `id_article`,
    `on_sale`,
    `deleted`,
    `attrs`,
    `created_at`,
    `updated_at`
    )

  SELECT
    `goods_id`,
    `goods_name`,
    NULL,
    `goods_weight` * 1000,
    '克',
    `goods_img`,
    `goods_thumb`,
    NULL,
    `is_on_sale`,
    `is_delete`,
    NULL,
    FROM_UNIXTIME(`add_time`),
    FROM_UNIXTIME(`last_update`)
  FROM
    `cn_goods`
```
