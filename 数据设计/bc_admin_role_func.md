# bc_admin_role_func 基本表

admin角色功能关联表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_admin_role_func`;

CREATE TABLE `bc_admin_role_func` (
  `id_role` int(11) NOT NULL COMMENT '角色id',
  `id_func` int(11) NOT NULL COMMENT '功能id',

  /* 数据审计 */
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_role`, `id_func`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='admin角色功能关联表';

```
