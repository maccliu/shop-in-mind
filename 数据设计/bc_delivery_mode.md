# bc_delivery_mode 基本表

送货方式。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_delivery_mode`;

CREATE TABLE `bc_delivery_mode` (
  `id_delivery_mode` int(11) NOT NULL,
  `name` varchar(40) NOT NULL COMMENT '名称',
  
  `id_warehouse` int(11) NOT NULL COMMENT '适用的发货仓库id',
  
  `currency` varchar(3) DEFAULT 'NZD' COMMENT '币种',
  `unit` varchar(10) DEFAULT '克' COMMENT '重量的单位',
  
  `init_weight` int(11) NOT NULL COMMENT '首重',
  `init_price` decimal(10,2) NOT NULL COMMENT '首重价格',
  `step_weight` int(11) NOT NULL COMMENT '次重',
  `step_price` decimal(10,2) NOT NULL COMMENT '次重价格',
  
  `disp_order` float DEFAULT '0' COMMENT '显示顺序',
  
  `notes` text COMMENT '备注',
  
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_delivery_mode`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='送货方式';

```

> 备注:
> 1. `disp_order` 默认是0，如果要让一个送货方式显示靠前，就要把这个值设的大一点即可。
> 2. “门店自提免快递费”，可以把首重设的很大，然后首重价格设为0。
> 3. “快递费一口价”，可以把首重设的很大，然后首重价格设为一口价的价格。
