# bc_warehouse 基本表

仓库设置表。

## SQL定义

```sql

/* 创建 bc_warehouse 基本表 */

DROP TABLE `bc_warehouse`;

CREATE TABLE `bc_warehouse` (
  `id_warehouse` int(11) NOT NULL COMMENT '仓库id',
  `warehouse_name` varchar(30) NOT NULL COMMENT '仓库名称',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id_warehouse`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='仓库';

```

> 备注:
> 1. 主键 `id_warehouse` 不是自动递增，使用时请注意。