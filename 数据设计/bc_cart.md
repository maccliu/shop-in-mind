# bc_cart 基本表

购物车。

## SQL定义

```sql
DROP TABLE IF EXISTS `bc_cart`;

CREATE TABLE `bc_cart` (
  `id_cart` int(11) NOT NULL AUTO_INCREMENT COMMENT '购物车id',
  `id_session` int(11) NOT NULL COMMENT '会话id',
  `id_user` int(11) DEFAULT NULL COMMENT '客户id',

  `status` tinyint(1) NOT NULL COMMENT '购物车状态',

  `id_warehouse` tinyint(4) DEFAULT NULL COMMENT '发货仓库id',
  `id_delivery_plan` tinyint(4) DEFAULT NULL COMMENT '配送方式id',

  `currency` char(3) DEFAULT 'NZD' COMMENT '结算币种',

  `to_name` varchar(40) DEFAULT NULL COMMENT '收件人姓名',
  `to_company` varchar(50) DEFAULT NULL COMMENT '收件人公司',
  `to_tel` varchar(30) DEFAULT NULL COMMENT '收件人电话',
  `to_idnumber` varchar(32) DEFAULT NULL COMMENT '收件人身份证号',

  `to_nation` varchar(64) DEFAULT NULL COMMENT '国家/行政区',
  `to_province` varchar(64) DEFAULT NULL COMMENT '省/州',
  `to_city` varchar(64) DEFAULT NULL COMMENT '城市',
  `to_district` varchar(64) DEFAULT NULL COMMENT '区/县',
  `to_address` varchar(255) DEFAULT NULL COMMENT '收件地址',
  `to_postcode` varchar(10) DEFAULT NULL COMMENT '邮编',

  `from_use` tinyint(1) NOT NULL DEFAULT '0' COMMENT '启用发件人',
  `from_name` varchar(40) DEFAULT NULL COMMENT '发件人姓名',
  `from_tel` varchar(30) DEFAULT NULL COMMENT '发件人电话',
  `from_address` varchar(255) DEFAULT NULL COMMENT '发件人地址',

  `with_photo` tinyint(1) DEFAULT '0' COMMENT '需要拍照',
  `with_sheet` tinyint(1) DEFAULT '0' COMMENT '需要面单',

  `id_referer` int(11) DEFAULT NULL COMMENT '本次购物的推荐人id',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_cart`),
  UNIQUE KEY `id_session` (`id_session`),
  KEY `id_user` (`id_user`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8 COMMENT='购物车';

```

> 备注：
> 1. `status` 购物车状态：0-正在使用 1-已作废 9-已生成订单。
> 2. 一个用户最多只准有1个状态为0(正在使用)的购物车。
> 3. id_referer是用于社会化营销场景的。如果本次购物是由某个推荐人推荐的，可以记录下来推荐人，用于给推荐人做推荐佣金。
