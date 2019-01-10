# bc_category_tree 基本表

品类树。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_category_tree`;

CREATE TABLE `bc_category_tree` (
    `category_id` INT(11) NOT NULL,
    `nodes` TEXT,

    PRIMARY KEY (`category_id`)
)  ENGINE=INNODB DEFAULT CHARSET=UTF8;

```

> 备注：
> 1. `nodes`为本品类和所有子孙品类的id列表，id间以逗号分隔