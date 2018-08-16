# bc_admin_role 基本表

admin角色表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_admin_role`;

CREATE TABLE `bc_admin_role` (
  `id_role` int(11) NOT NULL AUTO_INCREMENT COMMENT '角色id',
  `role_name` varchar(32) NOT NULL COMMENT '角色名',
  `sort_order` float DEFAULT '9999' COMMENT '顺序',
  `notes` text COMMENT '备注',

  /* 数据审计 */
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_role`),
  KEY `sort_order` (`sort_order`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='admin角色';

```
