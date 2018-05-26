# bc_detail_image 基本表

商品详情页的图片。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_detail_image`;

CREATE TABLE `bc_detail_image` (
  `id_detail_image` int(11) NOT NULL AUTO_INCREMENT,
  `id_detail` int(11) NOT NULL,
  `url` varchar(255) DEFAULT NULL COMMENT '图片url',
  `disp_order` float DEFAULT NULL COMMENT '显示顺序',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id_detail_image`),
  KEY `id_detail` (`id_detail`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品详情页图片';

```

> 备注：
> 1. 目前，各大电商平台的主流都是用图片来构造商品详情页。