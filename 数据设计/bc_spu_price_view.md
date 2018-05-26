# bc_spu_price_view 视图

商品价格视图。

创建 `bc_spu_price_view` 视图的目的是为了使用价格分层机制，运用组内排序技术，从数据库直接得到商品在特定条件下的价格。而实现组内排序，需要构造一个预先排序的派生表。因为这个派生表会被经常使用，所以直接将这个预排序的派生表定义成本视图，方便程序中调用。

## SQL定义

```sql

DROP VIEW IF EXISTS `bc_spu_price_view`;

CREATE VIEW `bc_spu_price_view` AS
  SELECT DISTINCT
    `bc_spu_price`.`id_price` AS `id_price`,

    `bc_spu_price`.`id_spu` AS `id_spu`,
    `bc_spu_price`.`id_warehouse` AS `id_warehouse`,
    `bc_spu_price`.`user_rank` AS `user_rank`,

    `bc_spu_price`.`price_type` AS `price_type`,
    `bc_spu_price`.`currency` AS `currency`,
    `bc_spu_price`.`price` AS `price`,
    `bc_spu_price`.`start_at` AS `start_at`,
    `bc_spu_price`.`end_at` AS `end_at`,
    `bc_spu_price`.`post_free` AS `post_free`,
    `bc_spu_price`.`price_tag` AS `price_tag`,

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
> 1. `bc_spu_price_view` 的 `SELECT` 中，必须要加上 `DISTINCT`，这是一个**技术核心**：不加DISTINCT的话，组内排序是无法实现的，`group by` 最终出来的结果会是mysql的默认排序，而不是我们希望的是按照指定字段排序。
