# bc_price_view 视图

商品价格视图。

创建 `bc_price_view` 视图的目的是为了使用价格分层机制，运用组内排序技术，从数据库直接得到商品在特定条件下的价格。而实现组内排序，需要构造一个预先排序的派生表。因为这个派生表会被经常使用，所以直接将这个预排序的派生表定义成本视图，方便程序中调用。

## SQL定义

```sql

DROP VIEW IF EXISTS `bc_price_view`;

CREATE VIEW `bc_price_view` AS

  SELECT DISTINCT
    `bc_price_pool`.`id_price` AS `id_price`,
    `bc_price_pool`.`id_spu` AS `id_spu`,

    `bc_price_pool`.`user_rank` AS `user_rank`,

    `bc_price_pool`.`price_level` AS `price_level`,

    'NZD' AS `currency`,
    (`bc_price_pool`.`price` * `bc_currency_rate`.`rate`) AS `price`,

    `bc_price_pool`.`start_at` AS `start_at`,
    `bc_price_pool`.`end_at` AS `end_at`,
    `bc_price_pool`.`post_free` AS `post_free`,
    `bc_price_pool`.`price_tag` AS `price_tag`,

    `bc_price_pool`.`updated_at` AS `updated_at`,
    `bc_price_pool`.`updated_by` AS `updated_by`
  FROM
    `bc_price_pool`
  INNER JOIN
    `bc_currency_rate`
      ON
        `bc_currency_rate`.`from` = `bc_price_pool`.`currency`
        AND `bc_currency_rate`.`to` = "NZD"
  ORDER BY
    `bc_price_pool`.`id_spu`,
    `bc_price_pool`.`price_level` DESC,
    `bc_price_pool`.`user_rank` DESC

;

```

> 备注:
> 1. `bc_price_view` 的 `SELECT` 中，必须要加上 `DISTINCT`，这是一个 **关键技术知识点** ：不加DISTINCT的话，对这个视图的组内排序是无法实现的，`group by` 最终出来的结果会是mysql的默认排序，而不是我们希望的是按照指定字段排序。
> 2. 本视图已经将币种全部转为NZD，方便代码中进行归一化处理。但是bc_price_pool中的原始价格数据还是保留定义的币种。
