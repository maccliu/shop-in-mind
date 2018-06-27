# bc_delivery_model 基本表

运价模板。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_delivery_model`;

CREATE TABLE `bc_delivery_model` (
  `id` int(11) NOT NULL,

  `name` varchar(40) NOT NULL COMMENT '名称',
  `range` varchar(255) DEFAULT NULL COMMENT '送货范围',

  `id_warehouse` int(11) NOT NULL COMMENT '适用的发货仓库id',
  `min_weight` int(11) NOT NULL DEFAULT '0' COMMENT '最低重量',
  `max_weight` int(11) NOT NULL DEFAULT '999999999' COMMENT '最大重量',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '币种',
  `unit` varchar(10) DEFAULT '克' COMMENT '重量的单位',

  `init_weight` int(11) NOT NULL COMMENT '首重',
  `init_price` decimal(10,2) NOT NULL COMMENT '首重价格',
  `step_weight` int(11) NOT NULL COMMENT '次重',
  `step_price` decimal(10,2) NOT NULL COMMENT '次重价格',

  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `remark` varchar(255) DEFAULT NULL COMMENT '备注',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id`),
  KEY `id_warehouse` (`id_warehouse`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='运价模板';

```

> 备注:
> 1. `disp_order` 默认是9999，如果要让一个送货方式显示靠前，就要把这个值设的小一点即可。
> 2. “门店自提免快递费”，可以把首重设的很大，然后首重价格设为0。
> 3. “快递费一口价”，可以把首重设的很大，然后首重价格设为一口价的价格。
