# bc_order_item 基本表

订单商品表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_item`;

CREATE TABLE `bc_order_item` (
  `id_order_item` int(11) NOT NULL AUTO_INCREMENT,
  `id_order` int(11) NOT NULL COMMENT '订单id',

  `id_spu` int(11) NOT NULL COMMENT '商品id',
  `title` varchar(255) NOT NULL COMMENT '商品名称',
  `qty` int(11) NOT NULL COMMENT '商品数量',
  `price` decimal(10,2) NOT NULL COMMENT '商品单价 以基准货币计',
  `weight` float NOT NULL COMMENT '商品毛重(克)',

  `status` tinyint(4) DEFAULT NULL COMMENT '状态',
  
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_order_item`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单商品表';

```

> 备注：
> 1. `status` : 1备货中 2已发货 3已收货 4已完成 5售后中 6售后完成
