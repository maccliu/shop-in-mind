# bc_category_spu 基本表

品类-商品关联表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_category_spu`;

CREATE TABLE `bc_category_spu` (
  `id_category` int(11) NOT NULL,
  `id_spu` int(11) NOT NULL,
  `disp_order` float DEFAULT '99999',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_category`,`id_spu`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```

## 导入数据

```sql

/*
  删除id_spu在1-20000间的商品
*/
DELETE FROM
  `bc_category_spu`
WHERE
  `id_spu` BETWEEN 1 AND 19999
;


/*
  新西兰仓的商品
*/
INSERT INTO
  `bc_category_spu`
  (
    `id_category`,
    `id_spu`
  )

  SELECT
    `cat_id`,
    `goods_id`
  FROM
    `cn_goods`
;


/*
  国内仓的商品
*/
INSERT INTO
  `bc_category_spu`
  (
    `id_category`,
    `id_spu`
  )

  SELECT
    `cat_id`,
    (`goods_id` + 10000)
  FROM
    `cn_goods`
;

```