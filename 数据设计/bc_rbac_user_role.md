# bc_rbac_user_role 基本表

RBAC之用户角色关联表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_rbac_user_role`;

CREATE TABLE `bc_rbac_user_role` (
  `id_user` int(11) NOT NULL COMMENT '用户id',
  `id_role` int(11) NOT NULL COMMENT '角色id',

  /* 数据审计 */
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_user`, `id_role`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户角色关联表';

```
