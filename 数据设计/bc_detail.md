# bc_detail 基本表

商品详情页。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_detail`;

CREATE TABLE `bc_detail` (
  `id_detail` int(11) NOT NULL AUTO_INCREMENT,
  `keywords` varchar(255) DEFAULT NULL COMMENT '关键字',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id_detail`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商品详情页';

```

> 备注：
> 1. 因为实际中，存在大量的多个商品共用一个详情页的情况，详情页的图片又是客户流量的消耗大户，所以要把详情页从商品中独立出来，商品spu中只指明使用哪个详情页。
