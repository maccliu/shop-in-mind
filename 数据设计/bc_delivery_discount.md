# bc_delivery_price 基本表

运费折扣表。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_delivery_discount`;

CREATE TABLE `bc_delivery_discount` (
  `delivery_discount_id` int(11) NOT NULL COMMENT '运费折扣id',
  `delivery_plan_id` int(11) NOT NULL COMMENT '配送方案id',

  `start_at` date NOT NULL DEFAULT '2000-01-01' COMMENT '开始时间',
  `end_at` date NOT NULL DEFAULT '2099-12-31' COMMENT '结束时间',

  `currency` char(3) NOT NULL DEFAULT 'NZD' COMMENT '购物金额的币种',
  `min_amount` decimal(12,2) NOT NULL COMMENT '最小购物金额',
  `max_amount` decimal(12,2) NOT NULL DEFAULT '999999999.99' COMMENT '最大购物金额',

  `rate` decimal(7,3) NOT NULL DEFAULT '100.000' COMMENT '折扣率%',

  `description` varchar(255) DEFAULT NULL COMMENT '说明',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`delivery_discount_id`),
  KEY `delivery_plan_id` (`delivery_plan_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='运费折扣表';

```

> 备注:
> 1. 日期判断规则为 `start_at` <= 当前时间 <= `end_at`.
> 2. 购物金额判断规则为 `min_amount` <= 商品金额 < `max_amount`。
> 3. rate默认是100%折扣, 即包邮. 如果想设为运费半价, 则rate设为50即可.
