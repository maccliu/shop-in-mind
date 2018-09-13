# bc_post_plan 基本表

物流方案。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_post_plan`;

CREATE TABLE `bc_post_plan` (
  `id_post_plan` int(11) NOT NULL,
  `id_warehouse` int(11) NOT NULL COMMENT '适用的发货仓库id',

  `title` varchar(255) NOT NULL COMMENT '标题',
  `carrier` varchar(50) DEFAULT NULL COMMENT '承运商',

  `currency` varchar(3) DEFAULT 'NZD' COMMENT '计价币种',
  `unit` varchar(10) DEFAULT '克' COMMENT '计价的重量单位',

  `disp_order` float DEFAULT '9999' COMMENT '显示顺序',

  `description` varchar(255) DEFAULT NULL COMMENT '备注',

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_post_plan`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='物流方案';

```

> 备注:
> 1. `disp_order` 默认是9999，如果要让一个送货方式显示靠前，就要把这个值设的小一点即可。
