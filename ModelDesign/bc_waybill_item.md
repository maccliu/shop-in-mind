# bc_waybill_item 基本表

运单条目。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_waybill_item`;

CREATE TABLE `bc_waybill_item` (
  `waybill_item_id` int(11) NOT NULL AUTO_INCREMENT,

  `waybill_id` varchar(18) NOT NULL COMMENT '运单id',

  `stu_id` int(11) NOT NULL COMMENT '商品id',
  `stu_title` varchar(255) NOT NULL COMMENT '商品名称',
  `stu_weight` float NOT NULL COMMENT '商品毛重(克)',

  `qty` int(11) unsigned NOT NULL COMMENT '商品数量',

  `status` tinyint(3) DEFAULT '0' COMMENT '状态',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`waybill_item_id`),
  KEY `waybill_id` (`waybill_id`),
  KEY `stu_id` (`stu_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='运单条目';

```

> 备注：
> 1. `status`：0-尚未处理 1xx-配货 2xx-打包 3xx-发货 4xx-运输中 5xx-确认中 8xx-售后 9xx-完成