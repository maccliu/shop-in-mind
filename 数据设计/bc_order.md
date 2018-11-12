# bc_order 基本表

订单主表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order`;

CREATE TABLE `bc_order` (
  /* 订单标识 */
  `order_id` varchar(18) NOT NULL COMMENT '订单id',
  `order_ref` varchar(32) DEFAULT NULL COMMENT '订单参考号',

  /* 订单来源 */
  `channel` tinyint(4) NOT NULL COMMENT '渠道：1网站 2代客下单 3小程序',
  `channel_order_id` int(11) NOT NULL COMMENT '渠道的订单id',
  `channel_order_ref` varchar(32) DEFAULT NULL COMMENT '渠道的订单参考号',

  /* 用户信息 */
  `user_id` int(11) NOT NULL COMMENT '客户id',
  `user_name` int(11) NOT NULL COMMENT '客户名',
  `user_rank` int(11) NOT NULL COMMENT '客户级别',
  `rank_discount` decimal(6,2) NOT NULL COMMENT '用户级别折扣率',
  `user_mobile` varchar(40) DEFAULT NULL COMMENT '用户手机',
  `user_email` varchar(60) DEFAULT NULL COMMENT '用户email',

  /* 物流信息 */
  `warehouse_id` tinyint(4) NOT NULL COMMENT '发货仓库id',
  `delivery_way_id` tinyint(4) NOT NULL COMMENT '送货方式id',
  `delivery_vendor` varchar(40) DEFAULT NULL COMMENT '快递公司名',
  `delivery_range` varchar(40) DEFAULT NULL COMMENT '送货区域',

  /* 收件人 */
  `to_name` varchar(40) DEFAULT NULL COMMENT '收件人姓名',
  `to_tel` varchar(30) DEFAULT NULL COMMENT '收件人电话',
  `to_company` varchar(50) DEFAULT NULL COMMENT '收件人公司',
  `to_idnumber` varchar(32) DEFAULT NULL COMMENT '收件人身份证号',
  `to_nation` varchar(64) DEFAULT NULL COMMENT '国家/行政区',
  `to_province` varchar(64) DEFAULT NULL COMMENT '省/州',
  `to_city` varchar(64) DEFAULT NULL COMMENT '城市',
  `to_district` varchar(64) DEFAULT NULL COMMENT '区/县',
  `to_address` varchar(255) DEFAULT NULL COMMENT '收件地址',
  `to_postcode` varchar(10) DEFAULT NULL COMMENT '邮编',

  /* 发件人 */
  `from_use` tinyint(1) NOT NULL DEFAULT '0' COMMENT '启用发件人',
  `from_name` varchar(40) DEFAULT NULL COMMENT '发件人姓名',
  `from_tel` varchar(30) DEFAULT NULL COMMENT '发件人电话',
  `from_address` varchar(255) DEFAULT NULL COMMENT '发件人地址',

  /* 物流选项 */
  `with_photo` tinyint(1) DEFAULT '0' COMMENT '需要拍照',
  `with_sheet` tinyint(1) DEFAULT '0' COMMENT '需要面单',

  /* 结算币种 */
  `order_currency` char(3) NOT NULL COMMENT '结算币种',
  `currency_rate` decimal(10,4) NOT NULL COMMENT '结算汇率',

  /* 结算 */
  `order_items_count` int(11) DEFAULT '0' COMMENT '订单商品总件数',
  `order_items_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '订单的商品总金额 以基准币种计',

  `order_weight` float DEFAULT '0' COMMENT '订单所有商品毛重(克)',
  `order_delivery_weight` float DEFAULT '0' COMMENT '订单快递计价毛重(克)',

  `order_discount_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '订单的折扣总金额 以基准币种计',
  `order_promotion_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '订单的促销总金额 以基准币种计',

  `order_delivery_fee` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '快递费 以基准币种计',
  `order_insure_fee` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '保价费 以基准币种计',

  `order_adjustment_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '客服的改价总金额 以基准币种计',

  `order_tax` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '订单的总税额 以基准币种计',

  `order_total_amount` decimal(12,2) NOT NULL DEFAULT '0.0000' COMMENT '订单总金额 以基准币种计',

  /* 营销 */
  `referer_id` int(11) DEFAULT NULL COMMENT '订单推荐人id',

  /* 数据审计 */
  `created_at` datetime DEFAULT NULL COMMENT '订单的创建时间',
  `closed_at` datetime DEFAULT NULL COMMENT '订单关闭时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`order_id`),
  UNIQUE KEY `order_ref` (`order_ref`),
  KEY `user_id` (`user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单';

```

> 备注：
> 1. 订单应该是记录下单时的所有相关信息的一个快照，要素应该都在订单上得到记录，冗余信息在这里是必须的。
> 2. 考虑到中老年客户和客服交互时，用纯数字交流最方便，歧义最少。从订单习惯来，可以采用一个极简版的 `order_ref`的生成策略： （yymmdd + hhmmss + 6位随机数字，共18位）。如果强调隐私，则建议额外新建个9位数字的随机参考号生成表（100 000 000 ~ 999 999 999），需要用的时候，就从表中取一个没有用过的。
> 3. 建议只使用19位纯数字的 `order_ref`，因为 `INT64` 的取值范围为 -9223372036854775808 ~ 9223372036854775807 (10^19)，或者无符号的 0 ~ 18446744073709551615 (10^20)。如果采用19位数字，必要时，可以将其由varchar升级到long int型，提高查询速度。

