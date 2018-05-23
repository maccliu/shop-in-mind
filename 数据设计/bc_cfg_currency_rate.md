# bc_cfg_currency_rate 基本表

汇率设置。

## SQL定义

```sql

/* 创建 bc_cfg_currency_rate 基本表 */

DROP TABLE IF EXISTS `bc_cfg_currency_rate`;

CREATE TABLE `bc_cfg_currency_rate` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `from` varchar(3) NOT NULL COMMENT '从...货币',
  `to` varchar(3) NOT NULL COMMENT '到...货币',
  `rate` float(10,4) NOT NULL COMMENT '汇率',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `currency_pair` (`from`,`to`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```

> 备注:
> 1. `from` 和 `to` 为国际标准货币代码，并使用大写字母。如人民币CNY，美元USD，日元JPY，新西兰元NZD等。