# bc_admin_func 基本表

admin功能点。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_admin_func`;

CREATE TABLE `bc_admin_func` (
  `id_func` int(11) NOT NULL AUTO_INCREMENT COMMENT '功能id',
  `id_func_group` int(11) NOT NULL DEFAULT '0' COMMENT '功能组id',

  `func_name` varchar(64) NOT NULL COMMENT '功能名称',
  `description` text COMMENT '功能说明',

  /* 对应的代码入口 */
  `url` varchar(255) DEFAULT NULL COMMENT 'URL',
  `controller` varchar(128) DEFAULT NULL COMMENT '控制器',
  `action` varchar(128) DEFAULT NULL COMMENT '方法名',

  /* 杂项 */
  `active` tinyint(1) DEFAULT '0' COMMENT '可用',
  `sort_order` float DEFAULT '9999' COMMENT '显示顺序',

  /* 数据审计 */
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_func`),
  KEY `sort_order` (`sort_order`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='admin功能';

```
