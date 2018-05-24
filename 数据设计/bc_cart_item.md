# bc_order_item 基本表

购物车商品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_cart_item`;

CREATE TABLE `bc_cart_item` (
  `id_cart_item` int(11) NOT NULL AUTO_INCREMENT,
  `id_cart` int(11) NOT NULL COMMENT '购物车id',
  `id_spu` int(11) NOT NULL COMMENT '商品id',
  `id_warehouse` tinyint(4) DEFAULT NULL COMMENT '发货仓',
  
  `qty` int(11) NOT NULL COMMENT '商品数量',
  `checked` tinyint(1) NOT NULL DEFAULT '1' COMMENT '选中',
  
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_cart_item`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='购物车商品';

```

> 备注：
> 1. `checked` : 用户在购物车中是否选中此商品。1-选中，0-不选，默认是选中。
