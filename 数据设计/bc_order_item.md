# bc_order_item 基本表

订单商品。

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
  `price_tag` varchar(40) DEFAULT NULL COMMENT '价格标签',
  
  `sale_type` tinyint(4) NOT NULL DEFAULT '0' COMMENT '销售类型',
  
  `status` tinyint(4) DEFAULT '0' COMMENT '状态',
  
  `id_delivery` int(11) DEFAULT NULL COMMENT '快递单id',
  
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_order_item`),
  KEY `id_order` (`id_order`),
  KEY `id_spu` (`id_spu`),
  KEY `id_delivery` (`id_delivery`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单商品';


```

> 备注：
> 1. `status` : 0-默认 1-备货中 2-已发货 3-已收货 4-已完成 5-售后中 6-售后完成
