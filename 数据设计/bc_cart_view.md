# bc_cart_view 视图

购物车。

## SQL定义

```sql

DROP VIEW IF EXISTS `bc_cart_view`;

CREATE VIEW `bc_cart_view` AS
SELECT
  `bc_cart`.`id_cart`,
  `bc_cart`.`id_session`,
  `bc_cart`.`id_user`,
  `bc_cart`.`status`,

  `bc_cart`.`id_warehouse`,
  `bc_cart`.`id_delivery_way`,
  `bc_cart`.`currency`,

  `bc_cart`.`to_name`,
  `bc_cart`.`to_company`,
  `bc_cart`.`to_tel`,
  `bc_cart`.`to_idnumber`,

  `bc_cart`.`to_nation`,
  `bc_cart`.`to_province`,
  `bc_cart`.`to_city`,
  `bc_cart`.`to_district`,
  `bc_cart`.`to_address`,
  `bc_cart`.`to_postcode`,

  `bc_cart`.`from_use`,
  `bc_cart`.`from_name`,
  `bc_cart`.`from_tel`,
  `bc_cart`.`from_address`,

  `bc_cart`.`with_photo`,
  `bc_cart`.`with_sheet`,

  `bc_cart`.`id_referer`,

  `bc_warehouse`.`warehouse_name`,

  `bc_delivery_way`.`vendor` AS `delivery_vendor`,
  `bc_delivery_way`.`range` AS `delivery_range`,
  `bc_delivery_way`.`currency` AS `delivery_currency`,
  `bc_delivery_way`.`init_weight`,
  `bc_delivery_way`.`init_price`,
  `bc_delivery_way`.`step_weight`,
  `bc_delivery_way`.`step_price`,

  `bc_cart`.`updated_at`
FROM
  `bc_cart`
LEFT JOIN
  `bc_warehouse`
    ON
      `bc_cart`.`id_warehouse` = `bc_warehouse`.`id_warehouse`
LEFT JOIN
  `bc_delivery_way`
    ON
      `bc_cart`.`id_delivery_way` = `bc_delivery_way`.`id_delivery_way`
;

```

