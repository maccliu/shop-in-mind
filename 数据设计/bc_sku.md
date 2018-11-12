# bc_sku 基本表

单品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_sku`;

CREATE TABLE `bc_sku` (
  `sku_id` INT(11) NOT NULL,
  `sku_code` VARCHAR(40) DEFAULT NULL COMMENT '本店货号',

  `sku_title` VARCHAR(255) NOT NULL COMMENT '单品标题',
  `brand_id` INT(11) DEFAULT NULL COMMENT '品牌id',

  `uom` VARCHAR(20) DEFAULT NULL COMMENT '销售单位',

  `weight` FLOAT DEFAULT NULL COMMENT '商品重量',
  `weight_unit` VARCHAR(16) DEFAULT NULL COMMENT '重量的计量单位',

  `image` VARCHAR(255) DEFAULT NULL COMMENT '单品主图',
  `small_image` VARCHAR(255) DEFAULT NULL COMMENT '单品小图',

  `on_sale` TINYINT(1) NOT NULL DEFAULT '0' COMMENT '上架',
  `deleted` TINYINT(1) NOT NULL DEFAULT '0' COMMENT '已删除',

  `barcode` VARCHAR(32) DEFAULT NULL COMMENT '条码',
  `barcode_type` VARCHAR(16) DEFAULT NULL COMMENT '条码类型',
  `qrcode` VARCHAR(240) DEFAULT NULL COMMENT '二维码',
  `qrcode_type` VARCHAR(16) DEFAULT NULL COMMENT '二维码类型',

  `attrs` TEXT COMMENT '单品参数 json格式',

  `created_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`sku_id`),
  UNIQUE KEY `sku_code` (`sku_code`),
  KEY `brand_id` (`brand_id`),
  KEY `qrcode` (`qrcode`),
  KEY `barcode` (`barcode`),
  KEY `sku_title` (`sku_title`)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;

```

> 备注
> 1. `sku`是作为库存、配货、发货的基本单位，不是销售的基本单位。`stu`才是作为销售基本单位。
