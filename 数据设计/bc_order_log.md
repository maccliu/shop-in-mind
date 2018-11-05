# bc_order_log 基本表

订单日志。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_log`;

CREATE TABLE `bc_order_log` (
  `id` int(11) NOT NULL AUTO_INCREMENT,

  `id_order` varchar(18) NOT NULL COMMENT '订单id',
  `log` varchar(255) NOT NULL COMMENT '日志内容',

  `by` varchar(30) DEFAULT NULL COMMENT '创建人',
  `by_type` varchar(10) DEFAULT NULL COMMENT '创建人的类型',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',

  PRIMARY KEY (`id`),
  KEY `id_order` (`id_order`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单日志';

```

> 备注：
> 1. `by_type` 可为 user, staff, system
