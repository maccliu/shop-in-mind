# bc_admin_user_role 基本表

admin用户角色关系表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_admin_user_role`;

CREATE TABLE `bc_admin_user_role` (
  `user_id` int(11) NOT NULL COMMENT '用户id',
  `role_id` int(11) NOT NULL COMMENT '角色id',

  /* 数据审计 */
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`user_id`, `role_id`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='admin用户角色关联表';

```
