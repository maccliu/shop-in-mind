# bc_user_favorite 基本表

用户收藏的商品。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_user_favorite`;

CREATE TABLE `bc_user_favorite` (
  `favorite_id` int(11) NOT NULL AUTO_INCREMENT,

  `user_id` int(11) NOT NULL COMMENT '客户id',
  `stu_id` int(11) NOT NULL COMMENT '商品id',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',

  PRIMARY KEY (`favorite_id`),
  UNIQUE KEY `uk1` (`user_id`,`stu_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

```
