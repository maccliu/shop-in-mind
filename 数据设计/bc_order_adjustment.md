# bc_order_adjustment 基本表

订单的调价记录。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_adjustment`;

CREATE TABLE `bc_order_adjustment` (
  `id_adjustment` int(11) NOT NULL AUTO_INCREMENT,
  `id_order` int(11) NOT NULL COMMENT '订单id',
  
  `amount` decimal(10,2) NOT NULL DEFAULT '0.00' COMMENT '调价金额 以基准货币计',
  `qty` int(11) NOT NULL DEFAULT '1' COMMENT '数量',
  `reason` varchar(255) DEFAULT NULL COMMENT '调价原因',
  
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  `updated_by` int(11) DEFAULT NULL COMMENT '客服id',
  
  PRIMARY KEY (`id_adjustment`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单的调价记录';

```

> 备注：
> 1. `amount` 加价用正数，降价用负数。比如西藏新疆快递费要额外加价，amount要填一个正数。对某个客户进行促销，对一个商品稍微降点价，amount就要用负数。
