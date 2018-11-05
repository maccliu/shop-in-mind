# bc_order_status 基本表

订单状态表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_status`;

CREATE TABLE `bc_order_status` (
  `id_order` varchar(18) NOT NULL COMMENT '订单id',

  /* 整体状态 */
  `status` tinyint(4) DEFAULT '1' COMMENT '订单状态',

  /* 支付状态 */
  `paid_status` tinyint(4) DEFAULT '0' COMMENT '支付状态',
  `paid_time` datetime DEFAULT NULL COMMENT '支付状态的更新时间',
  `pay_before` datetime DEFAULT NULL COMMENT '等待支付的截止时间',
  `order_total_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '订单总金额 以基准币种计',
  `order_paid_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '已支付金额 以基准币种计',

  /* 配货状态 */
  `pick_status` tinyint(4) DEFAULT '0' COMMENT '配货状态',
  `pick_time` datetime DEFAULT NULL COMMENT '配货状态的更新时间',

  /* 物流状态 */
  `delivery_status` tinyint(4) DEFAULT '0' COMMENT '物流状态',
  `delivery_time` datetime DEFAULT NULL COMMENT '物流状态的更新时间',

  /* 收货状态 */
  `received_status` tinyint(4) DEFAULT '0' COMMENT '收货状态',
  `received_time` datetime DEFAULT NULL COMMENT '收货状态的更新时间',

  /* 售后状态 */
  `service_status` tinyint(4) DEFAULT '0' COMMENT '售后状态',
  `service_time` datetime DEFAULT NULL COMMENT '售后状态的更新时间',

  PRIMARY KEY (`id_order`),
  KEY `status` (`status`),
  KEY `paid_status` (`paid_status`),
  KEY `pick_status` (`pick_status`),
  KEY `delivery_status` (`delivery_status`),
  KEY `received_status` (`received_status`),
  KEY `service_status` (`service_status`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单状态表';

```

> 备注：
> 1. 订单在执行过程中，状态会经常变化，按照数据动静分离原则，把订单的动态状态整合到一起，方便数据库优化。
> 2. 这个表是和bc_order表一起创建的。

## `status`

| `status` | 说明
|:--:|:--
| 0 | 已取消
| 1 | 待支付
| 2 | 待发货
| 3 | 待收货
| 4 | 待评价
| 5 | 有售后
| 9 | 完成
