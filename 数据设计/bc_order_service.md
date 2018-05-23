# bc_order_service 基本表

订单的售后服务记录。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_service`;

CREATE TABLE `bc_order_service` (
  `id_order_service` int(11) NOT NULL AUTO_INCREMENT,
  `id_order` int(11) NOT NULL COMMENT '订单id',
  
  `staff` varchar(30) DEFAULT NULL COMMENT '客服名字',
  `notes` text COMMENT '情况说明',
  
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_order_service`),
  KEY `id_order` (`id_order`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单售后';

```

> 备注：
> 1. 要把售后设为“完成”的话，一般是单独做个按钮，点按钮后，直接把对应订单的service_status设为已完成。
