# bc_rbac_user 基本表

RBAC之用户表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_rbac_user`;

CREATE TABLE `bc_rbac_user` (
  `id_user` int(11) NOT NULL AUTO_INCREMENT COMMENT '用户id',
  `user` varchar(32) NOT NULL COMMENT '用户名',
  `status` tinyint not null default '1' COMMENT '状态',
  `description` text,

  /* 数据审计 */
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_user`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户';

```

> 备注:
> 1. `status`: 0--已停用 1--正常