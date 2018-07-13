# bc_spu_group 基本表

商品组。

## SQL 定义

```sql
DROP TABLE IF EXISTS `bc_spu_group`;

CREATE TABLE `bc_spu_group` (
  `id_group` int(11) NOT NULL AUTO_INCREMENT,
  `code` varchar(60) DEFAULT NULL,

  `title` varchar(255) DEFAULT NULL COMMENT '标题',

  `banner` varchar(255) DEFAULT NULL COMMENT 'banner图片的url',
  `icon` varchar(255) DEFAULT NULL COMMENT 'icon图片的url',
  `tile` varchar(255) DEFAULT NULL COMMENT 'tile图片的url',

  `id_more` int(11) comment '更多',

  `mode` tinyint(4) NOT NULL DEFAULT '0' COMMENT '商品清单的模式 0-固定 1-SQL',
  `list` text COMMENT '固定的清单',
  `sql` text COMMENT 'SQL的表达式',
  `params` text COMMENT 'SQL的参数',

  `remark` text COMMENT '备注说明',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_group`),
  UNIQUE KEY `code_UNIQUE` (`code`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品组';
```

> 注：
> 1. `id_more` 很多时候，一个清单只是简单的列出几个典型商品，客户点击“更多”后，则显示`id_more`对应的商品列表，那个清单里面有更多商品。
> 2. `icon`是图标，`banner` 是横幅图，`tile`是方块图。这几种图分别对应不同的场合。
