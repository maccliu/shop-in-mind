# bc_cart_item_view 视图

购物车商品视图。

## SQL定义

```sql

DROP VIEW IF EXISTS `bc_cart_item_view`;

CREATE VIEW `bc_cart_item_view` AS
SELECT
  `bc_cart_item`.`cart_item_id` AS `cart_item_id`,
  `bc_cart_item`.`cart_id` AS `cart_id`,
  `bc_cart_item`.`stu_id` AS `stu_id`,
  `bc_cart_item`.`qty` AS `qty`,
  `bc_cart_item`.`checked` AS `checked`,

  `bc_stu`.`warehouse_id` AS `warehouse_id`,
  `bc_stu`.`title` AS `title`,
  `bc_stu`.`weight` AS `weight`,
  `bc_stu`.`weight_unit` AS `weight_unit`,
  `bc_stu`.`on_sale` AS `on_sale`,
  `bc_stu`.`deleted` AS `deleted`,
  `bc_stu`.`image` AS `image`,
  `bc_stu`.`thumb` AS `thumb`,
  `bc_stu`.`detail_id` AS `detail_id`,

  `bc_cart_item`.`created_at` AS `created_at`,
  `bc_cart_item`.`updated_at` AS `updated_at`
FROM
  `bc_cart_item`
INNER JOIN
  `bc_stu`
    ON
      `bc_cart_item`.`stu_id` = `bc_stu`.`stu_id`
INNER JOIN
  `bc_warehouse`
    ON
      `bc_stu`.`warehouse_id` = `bc_warehouse`.`warehouse_id`

```
