# bc_post_rule 基本表

运价规则。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_post_rule`;

CREATE TABLE `bc_post_rule` (
  `id_post_rule` int(11) NOT NULL,
  `id_warehouse` int(11) NOT NULL COMMENT '适用的发货仓库id',

  `title` varchar(255) NOT NULL COMMENT '标题',
  `carrier` varchar(50) DEFAULT NULL COMMENT '承运商',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '计价币种',
  `unit` varchar(10) DEFAULT '克' COMMENT '计价的重量单位',

  `rule` text COMMENT '运价规则，json格式',

  `disp_order` float DEFAULT '0' COMMENT '显示顺序',

  `remark` varchar(255) DEFAULT NULL COMMENT '备注',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_post_rule`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='运价规则';

```

> 备注:
> 1. `disp_order` 默认是9999，如果要让一个送货方式显示靠前，就要把这个值设的小一点即可。
> 2. “门店自提，免快递费”，可以把首重设的很大，然后首重价格设为0。
> 3. “快递费一口价”，可以把首重设的很大，然后首重价格设为一口价的价格。

## `rule`字段说明

```json
[
  {
    "min": 重量区间下限,
    "max": 重量区间上限,
    "init": 首重,
    "init_price": 首重价格,
    "step": 续重,
    "step_price": 续重价格,
  }
]
```

**示例1：新西兰，奥克兰市外**

* 2kg 以内 10纽币
* 2kg 至 5kg 19纽币
* 5kg 至 10kg 28纽币
* 10kg以上，每公斤加2.8纽币

```json
[
  {
    "min": 0,
    "max": 2000,
    "init": 2000,
    "init_price": 10
  },
  {
    "min": 2000,
    "max": 5000,
    "init": 5000,
    "init_price": 19
  },
  {
    "min": 5000,
    "max": 10000,
    "init": 10000,
    "init_price": 28
  },
  {
    "min": 10000,
    "max": 999999999,
    "init": 11000,
    "init_price": 30.8,
    "step": 1000,
    "step_price": 2.8
  }
]
```

**示例2：新西兰，奥克兰市内**

* 每25kg，5纽币

```json
[
  {
    "min": 0,
    "max": 999999999,
    "init": 25000,
    "init_price": 5,
    "step": 25000,
    "step_price": 5
  }
]
```

**示例3：新西兰直邮，富腾达，国内主区**

* 首重1公斤，3.99纽币；续重1公斤，4纽币

```json
[
  {
    "min": 0,
    "max": 999999999,
    "init": 1000,
    "init_price": 3.99,
    "step": 1000,
    "step_price": 4
  }
]
```

**示例4：门店自提**

* 免快递费

```json
[
  {
    "min": 0,
    "max": 999999999,
    "init": 999999999,
    "init_price": 0
  }
]
```

