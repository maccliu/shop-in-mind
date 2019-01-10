# bc_stu_sku 基本表

商品包含的单品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_stu_sku`;

CREATE TABLE `bc_stu_sku` (
  `stu_id` int(11) NOT NULL,
  `sku_id` int(11) NOT NULL,
  `qty` int(11) NOT NULL DEFAULT '1',

  `disp_order` float DEFAULT '0' COMMENT '显示顺序',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`stu_id`,`sku_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品包含的单品';

```
