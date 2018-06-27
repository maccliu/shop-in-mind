# bc_brand 基本表

品牌。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_brand`;

CREATE TABLE `bc_brand` (
  `id_brand` int(11) NOT NULL AUTO_INCREMENT COMMENT '品牌id',
  `brand_code` varchar(32) DEFAULT NULL COMMENT '品牌代码',

  `brand_name` varchar(64) NOT NULL COMMENT '品牌展示名',
  `brand_en` varchar(64) DEFAULT NULL COMMENT '品牌英文名',
  `brand_cn` varchar(64) DEFAULT NULL COMMENT '品牌中文名',

  `brand_logo` varchar(255) DEFAULT NULL COMMENT '品牌logo',

  `brand_url` varchar(255) DEFAULT NULL COMMENT '品牌官网',
  `brand_article` text COMMENT '品牌文案',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_brand`),
  UNIQUE KEY `brand_code` (`brand_code`),

  KEY `brand_name` (`brand_name`),
  KEY `brand_en` (`brand_en`),
  KEY `brand_cn` (`brand_cn`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='品牌';

```
