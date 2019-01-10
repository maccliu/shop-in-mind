# bc_stu_detail 基本表

商品详情。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_stu_detail`;

CREATE TABLE `bc_stu_detail` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `stu_id` int(11) NOT NULL,

  `type` tinyint(4) DEFAULT '1' COMMENT '类型',
  `pic` varchar(255) DEFAULT NULL COMMENT '图片url',

  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id`),
  KEY `stu_id` (`stu_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品详情';

```

> 备注
> 1. `type` 详情图片的类型：1-商品详情 2-使用方法 3-注意事项 4-有效期
