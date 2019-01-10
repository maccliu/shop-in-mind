# bc_delivery_plan 基本表

配送方案。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_delivery_plan`;

CREATE TABLE `bc_delivery_plan` (
  `delivery_plan_id` int(11) NOT NULL COMMENT '配送方案id',
  `warehouse_id` int(11) NOT NULL COMMENT '适用的发货仓库id',

  `title` varchar(255) NOT NULL COMMENT '标题',
  `carrier` varchar(50) DEFAULT NULL COMMENT '承运商',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '计价币种',
  `unit` varchar(10) DEFAULT '克' COMMENT '计价的重量单位',

  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `description` varchar(255) DEFAULT NULL COMMENT '说明',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`delivery_plan_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='配送方案';

```

> 备注:
> 1. `disp_order` 默认是9999，如果要让一个送货方式显示靠前，就要把这个值设的小一点即可。
