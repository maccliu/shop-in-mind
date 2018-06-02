# bc_cart_item_view 视图

购物车商品视图。

## SQL定义

```sql

DROP VIEW IF EXISTS `bc_cart_item_view`;

CREATE VIEW `bc_cart_item_view` AS
SELECT
  `bc_cart_item`.`id_cart_item` AS `id_cart_item`,
  `bc_cart_item`.`id_cart` AS `id_cart`,
  `bc_cart_item`.`id_spu` AS `id_spu`,
  `bc_cart_item`.`qty` AS `qty`,
  `bc_cart_item`.`checked` AS `checked`,

  `bc_spu`.`id_warehouse` AS `id_warehouse`,
  `bc_spu`.`title` AS `title`,
  `bc_spu`.`weight` AS `weight`,
  `bc_spu`.`weight_unit` AS `weight_unit`,
  `bc_spu`.`on_sale` AS `on_sale`,
  `bc_spu`.`deleted` AS `deleted`,
  `bc_spu`.`image` AS `image`,
  `bc_spu`.`thumb` AS `thumb`,
  `bc_spu`.`id_detail` AS `id_detail`,

  `bc_cart_item`.`created_at` AS `created_at`,
  `bc_cart_item`.`updated_at` AS `updated_at`
FROM
  `bc_cart_item`
INNER JOIN
  `bc_spu`
    ON
      `bc_cart_item`.`id_spu` = `bc_spu`.`id_spu`
INNER JOIN
  `bc_warehouse`
    ON
      `bc_spu`.`id_warehouse` = `bc_warehouse`.`id_warehouse`

```
