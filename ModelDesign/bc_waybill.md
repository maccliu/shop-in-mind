# bc_waybill 基本表

运单主表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_waybill`;

CREATE TABLE `bc_waybill` (
  `waybill_id` int(11) NOT NULL AUTO_INCREMENT COMMENT '运单id',

  /* 运单资料 */
  `waybill_carrier` varchar(50) DEFAULT NULL COMMENT '快递公司',
  `waybill_number` varchar(100) DEFAULT NULL COMMENT '快递单号',
  `waybill_type` varchar(20) DEFAULT NULL COMMENT '快递类型',

  /* 订单标识 */
  `order_id` varchar(18) NOT NULL COMMENT '订单id',

  /* 用户信息 */
  `user_id` int(11) NOT NULL COMMENT '客户id',
  `user_mobile` varchar(40) DEFAULT NULL COMMENT '客户手机',
  `user_email` varchar(60) DEFAULT NULL COMMENT '客户email',

  /* 发货仓 */
  `warehouse_id` tinyint(4) NOT NULL COMMENT '发货仓库id',

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

  /* 状态 */
  `status` tinyint(4) DEFAULT '0' COMMENT '运单状态',

  /* 数据审计 */
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`waybill_id`),
  KEY `order_id` (`order_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='运单';

```

> 备注：
> 1. `status`运单状态。
