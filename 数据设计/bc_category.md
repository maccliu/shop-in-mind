# bc_category 基本表

商品品类。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_category`;

CREATE TABLE `bc_category` (
  `id_category` int(11) NOT NULL AUTO_INCREMENT COMMENT '品类id',
  `category_name` varchar(64) NOT NULL COMMENT '品类名称',

  `id_parent` int(11) NOT NULL DEFAULT '0' COMMENT '父品类id',
  `level` tinyint(4) NOT NULL DEFAULT '1' COMMENT '品类的级别',
  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `article` text COMMENT '文案',

  `url_rewrite` varchar(255) DEFAULT NULL,
  `meta_title` varchar(255) DEFAULT NULL,
  `meta_keywords` varchar(255) DEFAULT NULL,
  `meta_desc` varchar(255) DEFAULT NULL,

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_category`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```
