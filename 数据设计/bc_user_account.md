# bc_user_account 基本表

用户的登录账号。

## SQL定义

```sql
DROP TABLE IF EXISTS `bc_user_account`;

CREATE TABLE `bc_user_account` (
  `id_user` int(11) NOT NULL,
  `user_name` varchar(32) DEFAULT NULL COMMENT '用户名',
  `mobile` varchar(16) DEFAULT NULL COMMENT '手机号',
  `mobile_confirmed_at` datetime DEFAULT NULL COMMENT '手机号的绑定时间',
  `email` varchar(80) DEFAULT NULL COMMENT 'email',
  `email_confirmed_at` datetime DEFAULT NULL COMMENT 'Email的绑定时间',
  `salt` varchar(32) DEFAULT NULL COMMENT 'salt',
  `mode` tinyint(4) DEFAULT NULL COMMENT '验密模式',
  `pwdhash` varchar(64) DEFAULT NULL COMMENT '密码hash',
  `wx_openid` varchar(64) DEFAULT NULL COMMENT '微信openid',
  `wx_unionid` varchar(64) DEFAULT NULL COMMENT '微信unionid',
  `wx_confirmed_at` datetime DEFAULT NULL COMMENT '微信的绑定时间',
  `deleted` tinyint(1) NOT NULL DEFAULT '0' COMMENT '已删除',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id_user`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户的登录账户';

```

> 备注：
> 1. `mobile`、`email`必须在绑定后才能登录。
> 2. 因为客户可能是从不同的渠道导入的（比如有淘宝渠道来的客户、有京东渠道来的用户、有自营商城来的客户、有微信小程序来的客户等），而各个渠道的验密算法又不一样，所以用 `mode` 来标识相应的验密模式。
> 3. 登录时，要验证一下`deleted`是否为`1`。
