# bc_user_favorite 基本表

用户收藏的商品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_user_favorite`;

CREATE TABLE `bc_user_favorite` (
  `id_favorite` int(11) NOT NULL AUTO_INCREMENT,

  `id_user` int(11) NOT NULL COMMENT '客户id',
  `id_spu` int(11) NOT NULL COMMENT '商品id',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',

  PRIMARY KEY (`id_favorite`),
  UNIQUE KEY `uk1` (`id_user`,`id_spu`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```
