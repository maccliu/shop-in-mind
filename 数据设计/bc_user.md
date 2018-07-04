# bc_user 基本表

用户

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_user`;

CREATE TABLE `bc_user` (
  `id_user` int(11) NOT NULL,
  `user_rank` tinyint(4) DEFAULT '6' COMMENT '用户等级',

  `nickname` varchar(32) DEFAULT NULL COMMENT '网名',
  `wx_id` varchar(30) DEFAULT NULL comment '微信号',

  `avatar` varchar(255) DEFAULT NULL COMMENT '头像',
  `gender` tinyint(1) DEFAULT '0' COMMENT '性别 0-未填 1-男 2-女',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_user`),
  KEY `user_rank` (`user_rank`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户';

```

> 备注:
> 1. 主键 `id_user` 不是自动递增，使用时请注意。
> 2. 把不可让用户修改的字段，如`user_rank`等放到最前面。