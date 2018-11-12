# bc_stu_quota 基本表

商品限购规则。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_stu_quota`;

CREATE TABLE `bc_stu_quota` (
  `quota_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'id',

  `stu_id` int(11) NOT NULL COMMENT '商品id',
  `min` int(11) NOT NULL DEFAULT '1' COMMENT '最小购买数量',
  `max` int(11) NOT NULL COMMENT '最大购买数量',

  `start_at` datetime NOT NULL DEFAULT '2000-01-01 00:00:00' COMMENT '开始时间',
  `end_at` datetime NOT NULL DEFAULT '2099-12-31 23:59:59' COMMENT '结束时间',

  `updated_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`quota_id`),
  KEY `start_at` (`start_at`),
  KEY `end_at` (`end_at`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品限购规则';

```

> 备注:
> 1. 商品限购是指对每张订单里面的某个单品的购买数量限制。