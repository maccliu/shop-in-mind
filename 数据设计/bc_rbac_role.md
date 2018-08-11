# bc_rbac_role 基本表

RBAC之角色表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_rbac_role`;

CREATE TABLE `bc_rbac_role` (
  `id_role` int(11) NOT NULL AUTO_INCREMENT COMMENT '角色id',
  `role` varchar(32) NOT NULL COMMENT '角色名',
  `description` text,

  /* 数据审计 */
  `created_at` datetime DEFAULT NULL COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_role`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='角色';

```
