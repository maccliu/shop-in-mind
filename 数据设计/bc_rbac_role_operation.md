# bc_rbac_role_operation 基本表

RBAC之角色操作关联表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_rbac_role_operation`;

CREATE TABLE `bc_rbac_role_operation` (
  `id_role` int(11) NOT NULL COMMENT '角色id',
  `id_operation` int(11) NOT NULL COMMENT '操作id',

  /* 数据审计 */
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_role`, `id_operation`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='角色操作关联表';

```
