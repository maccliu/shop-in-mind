# bc_delivery_zone 基本表

配送区域。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_delivery_zone`;

CREATE TABLE `bc_delivery_zone` (
  `delivery_zone_id` int(11) NOT NULL,

  `country` varchar(2) NOT NULL DEFAULT 'CN' COMMENT '国家代码',
  `zone_name` varchar(100) NOT NULL COMMENT '区域名称',
  `description` varchar(255) DEFAULT NULL COMMENT '说明',

  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`delivery_zone_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='配送区域';
```
