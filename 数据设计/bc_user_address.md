# bc_user_address 基本表

用户地址本。

## SQL定义

```sql

/* 创建 bc_user_address 基本表 */

DROP TABLE IF EXISTS `bc_user_address`;

CREATE TABLE `bc_user_address` (
  `address_id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL COMMENT '客户id',

  `is_from` tinyint(1) DEFAULT '0' COMMENT '发货地址',
  `is_to` tinyint(1) DEFAULT '0' COMMENT '收货地址',

  `name` varchar(64) DEFAULT NULL COMMENT '联系人姓名',
  `tel` varchar(32) DEFAULT NULL COMMENT '电话',
  `email` varchar(80) DEFAULT NULL COMMENT 'Email',
  `idcard_number` varchar(32) DEFAULT NULL COMMENT '联系人身份证号',
  `idcard_type` varchar(32) DEFAULT NULL COMMENT '联系人身份证类型',

  `nation` varchar(64) DEFAULT NULL COMMENT '国家',
  `province` varchar(64) DEFAULT NULL COMMENT '省/州',
  `city` varchar(64) DEFAULT NULL COMMENT '城市',
  `district` varchar(64) DEFAULT NULL COMMENT '区县',
  `address` varchar(255) NOT NULL COMMENT '地址',
  `postcode` varchar(12) DEFAULT NULL COMMENT '邮编',

  `disp_order` float DEFAULT '9999' COMMENT '显示序号',

  `last_time_from` datetime DEFAULT NULL COMMENT '最近使用时间,发件',
  `last_time_to` datetime DEFAULT NULL COMMENT '最近使用时间,收件',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id`),
  KEY `user_id` (`user_id`),
  KEY `name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```
