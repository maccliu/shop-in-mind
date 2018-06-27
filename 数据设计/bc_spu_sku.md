# bc_spu_sku 基本表

商品包含的单品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_spu_sku`;

CREATE TABLE `bc_spu_sku` (
  `id_spu` int(11) NOT NULL,
  `id_sku` int(11) NOT NULL,
  `qty` int(11) NOT NULL DEFAULT '1',

  `disp_order` float DEFAULT '0' COMMENT '显示顺序',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_spu`,`id_sku`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品包含的单品';

```
