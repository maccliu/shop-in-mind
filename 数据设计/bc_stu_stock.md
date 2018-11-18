# bc_stu_stock 基本表

商品库存池。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_stu_stock`;

CREATE TABLE `bc_stu_stock` (
  `stock_id` int(11) NOT NULL AUTO_INCREMENT,

  `stu_id` int(11) NOT NULL COMMENT '商品id',
  `stock_type` tinyint(1) NOT NULL COMMENT '库存类型',

  `stock_tag` varchar(40) NOT NULL COMMENT '库存标签',

  `stock` int(11) NOT NULL COMMENT '库存量',

  `stock_low` int(11) NOT NULL DEFAULT '10' COMMENT '低库存报警阈值',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`stock_id`),
  UNIQUE KEY `unique_stock` (`stu_id`,`stock_type`),
  KEY `stu_id` (`stu_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品库存表';

```

> 备注:
> 1. `stock_type`是库存类型，其中值为`0`是基本库存，每个商品都有这个类型。而值为`1-9`是促销活动专用库存，不是每个商品都有，可根据需要自行添加。
> 2. `stock_tag` 可以设置库存标签，比如说“基本”，“双11”等，供（价格-库存）关联时选择正确的库存。其中，`stock_type`=0的`stock_tag`固定为“基本”。
> 3. `stock_low` 低库存报警阈值算法是大于这个设定值，比如阈值设定为10，那么当库存量为10，9，8，7...时都会报low，而11则不会报警。
> 4. 基本库存不可删除，专用库存可删除。专用库存删除时，其剩余库存会被转入到基本库存。

```
