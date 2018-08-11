# bc_rbac_operation 基本表

RBAC之操作表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_rbac_operation`;

CREATE TABLE `bc_rbac_operation` (
  `id_operation` int(11) NOT NULL AUTO_INCREMENT COMMENT '操作id',
  `operation` varchar(32) NOT NULL COMMENT '操作名',
  `description` text,

  /* 对应的代码入口 */
  `class_name` varchar(128) DEFAULT NULL COMMENT '类名',
  `method_name` varchar(128) DEFAULT NULL COMMENT '方法名',

  /* 数据审计 */
  `created_at` datetime DEFAULT NULL COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_operation`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='操作';

```
