# bc_cms_block 基本表

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_cms_block`;

CREATE TABLE `bc_cms_block` (
  `id_block` int(11) NOT NULL,
  
  `title` varchar(40) DEFAULT NULL COMMENT '标题',
  `subtitle` varchar(100) DEFAULT NULL COMMENT '副标题',
  
  `sql` text COMMENT '商品选择(SQL)',
  `notes` text COMMENT '备注',
  `mock` blob COMMENT '演示数据',
  
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  
  PRIMARY KEY (`id_block`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='展示区块';

```
