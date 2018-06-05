# bc_wxpay_notify 基本表

微信支付结果通知。 参考文档： <https://pay.weixin.qq.com/wiki/doc/api/wxa/wxa_api.php?chapter=9_7>

## SQL定义

```sql

DROP TABLE `bc_wxpay_notify`;

CREATE TABLE `bc_wxpay_notify` (
  `id` int(11) NOT NULL AUTO_INCREMENT,

  `out_trade_no` varchar(32) DEFAULT NULL COMMENT '商户订单号',
  `transaction_id` varchar(32) NOT NULL COMMENT '微信支付交易id',
  `fee_type` varchar(8) DEFAULT NULL COMMENT '币种',
  `total_fee` int(11) DEFAULT NULL COMMENT '交易金额(分)',

  `check_sign` tinyint(1) DEFAULT NULL COMMENT '签名验证成功',

  `xml` blob COMMENT '报文原文xml',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',

  PRIMARY KEY (`id`),
  KEY `out_trade_no` (`out_trade_no`),
  KEY `transaction_id` (`transaction_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='微信支付结果通知';

```

> 备注:
> 1. 收到一条就记录一条。
> 2. 对于同一条支付交易，微信可能会根据策略，发送多次通知，要能处理这种情况。
