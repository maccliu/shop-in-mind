# bc_order_payment 基本表

订单的支付记录。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_payment`;

CREATE TABLE `bc_order_payment` (
  `id_payment` int(11) NOT NULL,
  `id_order` int(11) NOT NULL COMMENT '订单id',

  `currency` varchar(3) NOT NULL COMMENT '支付币种',
  `amount` decimal(15,4) NOT NULL COMMENT '金额',

  `payment_method` varchar(20) NOT NULL COMMENT '支付方式',
  `id_reference` int(11) DEFAULT NULL COMMENT '支付记录的检索id',
  `data` blob COMMENT '相关数据',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',

  PRIMARY KEY (`id_payment`),
  KEY `id_order` (`id_order`),
  KEY `id_reference` (`id_reference`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单支付记录';

```

> 备注：
> 1. 一个订单可能有多条支付记录，比如一个订单应付100元，客户可以用（代金券70元 + 账户余额10元 + 微信支付20元）来完成整个订单的支付。
> 2. `id_reference`根据支付方式的不同，指向到不同的支付表的id。比如代金券的支付，指向到代金券的数据表的对应id；微信支付，指向到微信支付的数据表的对应id。
