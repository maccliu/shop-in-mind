# bc_order 基本表

订单主表。

## SQL定义

```sql
DROP TABLE IF EXISTS `bc_order`;

CREATE TABLE `bc_order` (
  `id_order` int(11) NOT NULL AUTO_INCREMENT COMMENT '订单id',
  `order_ref` varchar(16) DEFAULT NULL COMMENT '订单参考号',
  
  `status` tinyint(4) NOT NULL COMMENT '订单状态',
  
  `channel` tinyint(4) NOT NULL COMMENT '渠道：1网站 2代客下单 3小程序',
  `channel_order_id` int(11) NOT NULL COMMENT '渠道的订单id',
  `channel_order_ref` varchar(32) DEFAULT NULL COMMENT '渠道的订单参考号',
  
  `id_user` int(11) NOT NULL COMMENT '客户id',
  `id_cart` int(11) NOT NULL COMMENT '购物车id',
  `id_warehouse` tinyint(4) NOT NULL COMMENT '发货仓库id',
  `id_delivery_way` int(11) NOT NULL COMMENT '交货方式id',
  
  `order_currency` char(3) NOT NULL COMMENT '订单币种',
  `currency_rate` decimal(10,4) NOT NULL COMMENT '当时汇率',
  
  `order_items_amount` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '订单的商品金额 以基准币种计',
  `order_tax` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '订单的税额 以基准币种计',
  `order_discount_amount` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '订单的购物折扣金额 以基准币种计',
  `order_delivery_fee` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '快递费 以基准币种计',
  `order_insure_fee` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '保价费 以基准币种计',
  `order_adjustment_amount` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '客服的调价金额 以基准币种计',
  
  `order_payable_amount` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '订单应付总金额 以基准币种计',
  `order_paid_amount` decimal(15,4) NOT NULL DEFAULT '0.0000' COMMENT '已支付金额 以基准币种计',
  
  `to_name` varchar(40) DEFAULT NULL COMMENT '收件人姓名',
  `to_tel` varchar(30) DEFAULT NULL COMMENT '收件人电话',
  `to_company` varchar(100) DEFAULT NULL COMMENT '收件人公司',
  
  `to_nation` varchar(64) DEFAULT NULL COMMENT '国家/行政区',
  `to_province` varchar(64) DEFAULT NULL COMMENT '省/州',
  `to_city` varchar(64) DEFAULT NULL COMMENT '城市',
  `to_district` varchar(64) DEFAULT NULL COMMENT '区/县',
  `to_address` varchar(255) DEFAULT NULL COMMENT '收件地址',
  `to_postcode` varchar(10) DEFAULT NULL COMMENT '邮编',
  `to_idcard` varchar(32) DEFAULT NULL COMMENT '收件人身份证号',
  
  `from_name` varchar(40) DEFAULT NULL COMMENT '发件人姓名',
  `from_tel` varchar(30) DEFAULT NULL COMMENT '发件人电话',
  
  `with_photo` tinyint(1) DEFAULT '0' COMMENT '需要拍照',
  `with_sheet` tinyint(1) DEFAULT '0' COMMENT '需要面单',
  
  `id_referer` int(11) DEFAULT NULL COMMENT '订单推荐人id',
  
  `created_at` datetime DEFAULT NULL COMMENT '订单的创建时间',
  `pay_before` datetime DEFAULT NULL COMMENT '等待支付的截止时间',
  `paid_at` datetime DEFAULT NULL COMMENT '支付完成时间',
  `sent_at` datetime DEFAULT NULL COMMENT '发货时间',
  `received_at` datetime DEFAULT NULL COMMENT '收货时间',
  `closed_at` datetime DEFAULT NULL COMMENT '订单关闭时间',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_order`),
  UNIQUE KEY `order_ref` (`order_ref`),
  KEY `id_user` (`id_user`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单';

```