# bc_admin_user 基本表

admin用户。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_admin_user`;

CREATE TABLE `bc_admin_user` (
  `id_user` int(11) NOT NULL AUTO_INCREMENT COMMENT '用户id',
  `user_name` varchar(64) NOT NULL COMMENT '用户姓名',

  /* 登录 */
  `account` varchar(32) NOT NULL COMMENT '登录账号',
  `salt` varchar(16) NOT NULL COMMENT 'salt',
  `pwdhash` varchar(64) NOT NULL COMMENT '密码hash',

  /* 杂项 */
  `status` tinyint(4) NOT NULL DEFAULT '1' COMMENT '状态',
  `notes` text COMMENT '备注',

  /* 数据审计 */
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',

  PRIMARY KEY (`id_user`),
  UNIQUE KEY `account` (`account`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='admin用户';

```

> 备注:
> 1. `status`: 0--已停用 1--正常
> 2. `pwdhash`: md5(`salt`+`密码明文`)

> 登录验证步骤:
> 1. 前端提交要登录的`账号名account`。
> 2. 后台验证此`账号名account`是否存在? 是否有效? 如果不存在或者无效, 向前端输出错误信息后结束。
> 3. 如果账号有效, 后台向前端返回 `时间戳ts`+`账号对应的salt`。
> 4. 前端向后台提交 `账号`+`时间戳ts`+`计算出来的hash`。hash的计算规则为: 第一步: md5(`salt`+`密码明文`) => `hash1` 第二步: md5(`hash1`+`ts`) => `hash`。
> 5. 后台收到后, 首先检查`时间戳ts`和当前时间的差值是否处于合理区间(比如在90秒内)? 如果不对, 则说明可能是异常登录, 直接予以拒绝.
> 6. 如果时间戳在合理区间, 则从后台数据库中取出对应的admin_user的数据, 计算对应的 md5(`pwdhash`+`ts`), 然后和前台提交过来的`hash`做比对.
> 7. 如果一次性比对成功, 则此用户身份可被认证.
> 8. 如果比对失败, 则延迟0.5秒, 然后向前端发出错误信息.
