# bc_post_rule 基本表

运价规则。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_post_rule`;

CREATE TABLE `bc_post_rule` (
  `id_post_rule` int(11) NOT NULL AUTO_INCREMENT COMMENT '物流规则id',
  `id_post_plan` int(11) NOT NULL COMMENT '物流方案id',

  `min` int(11) NOT NULL DEFAULT '0' COMMENT '最小重量',
  `max` int(11) NOT NULL DEFAULT '999999' COMMENT '最大重量',

  `init` int(11) NOT NULL COMMENT '首重重量',
  `init_price` decimal(12,2) NOT NULL COMMENT '首重价格',
  `step` int(11) DEFAULT NULL COMMENT '续重重量',
  `step_price` decimal(12,2) DEFAULT NULL COMMENT '续重价格',

  `description` varchar(255) DEFAULT NULL COMMENT '说明',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_post_rule`),
  KEY `id_post_plan` (`id_post_plan`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='物流规则';
```

> 备注:
> 1. 重量判断规则为 `min` <= 重量 < `max`，即不包含最大重量。
> 2. “门店自提，免快递费”，可以把首重设的很大，然后首重价格设为0。
> 3. “快递费一口价”，可以把首重设的很大，然后首重价格设为一口价的价格。