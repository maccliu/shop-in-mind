# bc_admin_func_group 基本表

admin功能组。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_admin_func_group`;

CREATE TABLE `bc_admin_func_group` (
  `id_func_group` int(11) NOT NULL AUTO_INCREMENT COMMENT '功能组id',
  `group_name` varchar(64) NOT NULL COMMENT '功能组名称',
  `sort_order` float DEFAULT '9999' COMMENT '显示顺序',

  /* 数据审计 */
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_func_group`),
  KEY `sort_order` (`sort_order`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='admin功能组';

```
