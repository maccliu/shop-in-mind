# bc_stu_album 基本表

商品相册。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_stu_album`;

CREATE TABLE `bc_stu_album` (
  `image_id` int(11) NOT NULL AUTO_INCREMENT,

  `stu_id` int(11) NOT NULL COMMENT '商品id',

  `image_type` tinyint(1) DEFAULT '1' COMMENT '图片类型',
  `image_url` varchar(255) DEFAULT NULL COMMENT '图片url',

  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`image_id`),
  KEY `stu_id` (`stu_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品相册';

```

> 备注:
> 1. `image_type` 1-图片 2-视频