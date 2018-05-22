# bc_spu_price_view 视图

## SQL定义

```sql

/* 创建 bc_spu_price_view 视图 */
DROP VIEW IF EXISTS `bc_spu_price_view`;
CREATE VIEW `bc_spu_price_view` AS
  SELECT DISTINCT
    `bc_spu_price`.`id` AS `id`,
    `bc_spu_price`.`id_spu` AS `id_spu`,
    `bc_spu_price`.`price_type` AS `price_type`,
    `bc_spu_price`.`user_rank` AS `user_rank`,
    `bc_spu_price`.`id_warehouse` AS `id_warehouse`,
    `bc_spu_price`.`currency` AS `currency`,
    `bc_spu_price`.`price` AS `price`,
    `bc_spu_price`.`start_at` AS `start_at`,
    `bc_spu_price`.`end_at` AS `end_at`,
    `bc_spu_price`.`post_free` AS `post_free`,
    `bc_spu_price`.`updated_at` AS `updated_at`,
    `bc_spu_price`.`updated_by` AS `updated_by`
  FROM
    `bc_spu_price`
  ORDER BY
    `bc_spu_price`.`id_spu` ,
    `bc_spu_price`.`price_type` DESC ,
    `bc_spu_price`.`user_rank` DESC ,
    `bc_spu_price`.`id_warehouse` DESC
;
```

> 备注:
> 1. `bc_spu_price_view` 的 `SELECT` 中，必须要加上 `DISTINCT`，这是一个**技术核心**：不加DISTINCT的话，组内排序是无法实现的，`group by` 最终出来的结果会是mysql的默认排序，而不是我们希望的是按照指定字段`order by`。
