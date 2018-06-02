# bc_order_status 基本表

订单状态表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_status`;

CREATE TABLE `bc_order_status` (
  `id_order` int(11) NOT NULL COMMENT '订单id',

  `status` tinyint default '0' COMMENT '订单整体状态',

  `payment_status` tinyint(4) DEFAULT '0' COMMENT '支付状态',
  `payment_time` datetime DEFAULT NULL COMMENT '支付状态的更新时间',

  `pick_status` tinyint(4) DEFAULT '0' COMMENT '配货状态',
  `pick_time` datetime DEFAULT NULL COMMENT '配货状态的更新时间',

  `delivery_status` tinyint(4) DEFAULT '0' COMMENT '物流状态',
  `delivery_time` datetime DEFAULT NULL COMMENT '物流状态的更新时间',

  `service_status` tinyint(4) DEFAULT '0' COMMENT '售后状态',
  `service_time` datetime DEFAULT NULL COMMENT '售后状态的更新时间',

  PRIMARY KEY (`id_order`),
  KEY `status` (`status`),
  KEY `payment_status` (`payment_status`),
  KEY `pick_status` (`pick_status`),
  KEY `delivery_status` (`delivery_status`),
  KEY `service_status` (`service_status`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单状态表';

```

> 备注：
> 1. 订单在执行中，状态经常会变化，所以按照数据动静分离原则，把订单的动态状态整合到一起，方便快速查询。