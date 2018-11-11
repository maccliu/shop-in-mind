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
  `birthday` date DEFAULT NULL COMMENT '生日',

  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_user`),
  KEY `user_rank` (`user_rank`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户';

```

> 备注:
> 1. 主键 `id_user` 不是自动递增，使用时请注意。
> 2. 把不可让用户修改的字段，如`user_rank`等放到最前面。
> 3. 把用户表分为 `bc_user` 和 用户账号表 `bc_account`。`bc_user`存放的是用户的基本信息，可以输出给客户端的；而`bc_user_account`存放的是用户账号密码等机密信息，绝对禁止输出给客户端。分为两个表，可以避免开发人员无意中直接 `SELECT * FROM bc_user` ，然后输出到用户端，导致客户的机密信息泄露。