# bc_order_payment 基本表

订单的支付记录。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_payment`;

CREATE TABLE `bc_order_payment` (
  `order_payment_id` int(11) NOT NULL AUTO_INCREMENT,

  `order_id` varchar(18) NOT NULL COMMENT '订单id',
  `order_ref` varchar(32) DEFAULT NULL COMMENT '订单参考号',

  `user_id` int(11) NOT NULL COMMENT '用户id',
  `user_name` varchar(64) DEFAULT NULL COMMENT '用户名',

  `currency` varchar(3) NOT NULL COMMENT '支付币种',
  `amount` decimal(12,2) NOT NULL COMMENT '金额',

  `currency_rate` decimal(10,4) NOT NULL DEFAULT '1.0000' COMMENT '当时汇率',

  `payment_method` varchar(20) NOT NULL COMMENT '支付方式',
  `payment_ref` varchar(32) DEFAULT NULL COMMENT '支付参考号',

  `paid_at` datetime NOT NULL COMMENT '支付完成的时间',
  `bank_code` varchar(30) DEFAULT NULL COMMENT '银行代码',

  `payment_data` blob COMMENT '支付的相关数据',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',

  PRIMARY KEY (`order_payment_id`),
  UNIQUE KEY `payment_ref` (`payment_method`,`payment_ref`),
  KEY `order_id` (`order_id`),
  KEY `order_ref` (`order_ref`),
  KEY `user_id` (`user_id`),
  KEY `user_name` (`user_name`),
  KEY `paid_at` (`paid_at`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单支付记录';

```

> 备注：
> 1. 一个订单可能有多条支付记录，比如一个订单应付100元，客户可以用（代金券70元 + 账户余额10元 + 微信支付20元）来完成整个订单的支付。
> 2. 根据payment_method的不同，payment_ref指向到不同的支付表的id。比如微信支付，指向到微信支付日志的对应id；支付宝支付，指向到支付宝日志的对应id；代金券的支付，指向到代金券日志的对应id。
> 3. `payment_data`存放本次支付的详细数据，通常是支付服务商返回的详细支付数据。数据建议以json格式存放，便于以后将此字段升级为json型字段。