# bc_delivery_price 基本表

运价表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_delivery_price`;

CREATE TABLE `bc_delivery_price` (
  `delivery_price_id` int(11) NOT NULL AUTO_INCREMENT COMMENT '物流规则id',
  `delivery_plan_id` int(11) NOT NULL COMMENT '物流方案id',

  `min` int(11) NOT NULL DEFAULT '0' COMMENT '最小重量',
  `max` int(11) NOT NULL DEFAULT '999999' COMMENT '最大重量',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '币种',

  `init` int(11) NOT NULL COMMENT '首重重量',
  `init_price` decimal(12,2) NOT NULL COMMENT '首重价格',
  `step` int(11) DEFAULT NULL COMMENT '续重重量',
  `step_price` decimal(12,2) DEFAULT NULL COMMENT '续重价格',

  `description` varchar(255) DEFAULT NULL COMMENT '说明',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`delivery_price_id`),
  KEY `delivery_plan_id` (`delivery_plan_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='配送价格';
```

> 备注:
> 1. 重量判断规则为 `min` <= 重量 < `max`，即不包含最大重量。
> 2. “门店自提，免快递费”，可以把首重设的很大，然后首重价格设为0。
> 3. “快递费一口价”，可以把首重设的很大，然后首重价格设为一口价的价格。