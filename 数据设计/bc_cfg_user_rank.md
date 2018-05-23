# bc_cfg_user_rank 基本表

用户等级设置。

## SQL定义

```sql

/* 创建 bc_cfg_user_rank 基本表 */
DROP TABLE IF EXISTS `bc_cfg_user_rank`;
CREATE TABLE `bc_cfg_user_rank` (
  `id_rank` tinyint(4) NOT NULL,
  `rank_name` varchar(30) NOT NULL COMMENT '级别名称',
  `discount` float(5,2) unsigned NOT NULL DEFAULT '0.00' COMMENT '折扣率',
  `min_credit` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '信用点数下限',
  `max_credit` int(10) unsigned NOT NULL DEFAULT '0' COMMENT '信用点数上限',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id_rank`),
  KEY `min_credit` (`min_credit`),
  KEY `max_credit` (`max_credit`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```

> 备注:
> 1. 主键 `id_rank` 不是自动递增，使用时请注意。