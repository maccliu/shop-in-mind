# bc_user_rank 基本表

用户级别设置表。

## SQL定义

```sql

/* 创建 bc_user_rank 基本表 */

DROP TABLE IF EXISTS `bc_user_rank`;

CREATE TABLE `bc_user_rank` (
  `rank_id` tinyint(4) NOT NULL,
  `rank_name` varchar(30) NOT NULL COMMENT '级别名称',
  `discount` float(5,2) unsigned NOT NULL DEFAULT '0.00' COMMENT '折扣率',
  `min_credits` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '购物积分下限',
  `max_credits` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '购物积分上限',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`rank_id`),
  KEY `min_credits` (`min_credits`),
  KEY `max_credits` (`max_credits`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```

> 备注:
> 1. 主键 `rank_id` 不是自动递增，使用时请注意。