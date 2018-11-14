# bc_order_item 基本表

订单商品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_order_item`;

CREATE TABLE `bc_order_item` (
  `order_item_id` int(11) NOT NULL AUTO_INCREMENT,
  `order_id` varchar(18) NOT NULL COMMENT '订单id',

  `stu_id` int(11) NOT NULL COMMENT '商品id',
  `title` varchar(255) NOT NULL COMMENT '商品名称',
  `qty` int(11) unsigned NOT NULL COMMENT '商品数量',

  `weight` float NOT NULL COMMENT '商品毛重(克)',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '基准币种',
  `price` decimal(10,2) NOT NULL COMMENT '商品单价 以基准币种计',
  `price_type` tinyint(4) DEFAULT NULL COMMENT '价格类型：10日常价 20仓库价 30促销价 40节日价',
  `start_at` datetime DEFAULT NULL COMMENT '价格的开始时间',
  `end_at` datetime DEFAULT NULL COMMENT '价格的截止时间',
  `free_shipping` tinyint(4) NOT NULL DEFAULT '0' COMMENT '包邮:1包邮 0不包邮',
  `price_tag` varchar(40) DEFAULT NULL COMMENT '价格标签',

  `sale_type` tinyint(4) NOT NULL DEFAULT '0' COMMENT '销售类型',

  `status` tinyint(4) DEFAULT '0' COMMENT '状态',

  `delivery_id` int(11) DEFAULT NULL COMMENT '对应的快递单id',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`order_item_id`),
  KEY `order_id` (`order_id`),
  KEY `stu_id` (`stu_id`),
  KEY `delivery_id` (`delivery_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='订单商品';

```

> 备注：
> 1. `status` : 0-默认 1-备货中 2-已发货 3-已收货 4-已完成 5-售后中 6-售后完成
> 2. `sale_type`: 0-正常销售 1-促销 2-赠品
