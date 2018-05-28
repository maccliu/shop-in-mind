# bc_cart 基本表

购物车。

## SQL定义

```sql
DROP TABLE IF EXISTS `bc_cart`;

CREATE TABLE `bc_cart` (
  `id_cart` int(11) NOT NULL AUTO_INCREMENT COMMENT '购物车id',
  `id_session` int(11) NOT NULL COMMENT 'session',
  `id_user` int(11) DEFAULT NULL COMMENT '客户id',
  `status` tinyint(1) NOT NULL COMMENT '购物车状态',
  
  `id_warehouse` tinyint(4) DEFAULT NULL COMMENT '发货仓库id',
  `id_delivery_way` tinyint(4) DEFAULT NULL COMMENT '送货方式id',
  `currency` char(3) NOT NULL COMMENT '结算币种',
  
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
  
  `id_referer` int(11) DEFAULT NULL COMMENT '推荐人id',
  
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_cart`),
  UNIQUE KEY `id_session` (`id_session`),
  KEY `id_user` (`id_user`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='购物车';

```

> 备注：
> 1. `status` 购物车状态：0-正常 9-完成
