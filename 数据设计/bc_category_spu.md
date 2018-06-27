# bc_category_spu 基本表

品类-商品关联库。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_category_spu`;

CREATE TABLE `bc_category_spu` (
    `id_category` INT(11) NOT NULL,
    `id_spu` INT(11) NOT NULL,
    `disp_order` FLOAT DEFAULT '99999',

    `updated_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

    PRIMARY KEY (`id_category` , `id_spu`)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;

```
