# bc_session 基本表

客户会话。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_session`;

CREATE TABLE `bc_session` (
  `id_session` int(11) NOT NULL AUTO_INCREMENT,
  `id_channel` tinyint(4) NOT NULL COMMENT '渠道id',
  `id_user` int(11) DEFAULT NULL COMMENT '用户id',
  `token` varchar(32) NOT NULL COMMENT 'token',
  `ip` varchar(64) DEFAULT NULL COMMENT '客户端ip',

  `key1` varchar(64) DEFAULT NULL,
  `key2` varchar(64) DEFAULT NULL,
  `key3` varchar(64) DEFAULT NULL,

  `data1` varchar(255) DEFAULT NULL,
  `data2` varchar(255) DEFAULT NULL,
  `data3` varchar(255) DEFAULT NULL,

  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,

  PRIMARY KEY (`id_session`),
  KEY `id_user` (`id_user`),
  KEY `key1` (`key1`),
  KEY `key2` (`key2`),
  KEY `key3` (`key3`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='客户会话';

```

> 备注：
> 1. `token` 是随机生成的字符串，用于检查（客户端和app）之间的通讯数据是否可信。
> 2. `key1`、`key2`、`key3` 保留字段，用于不同的 channel 对应的会话关键字段，有索引。比如对于微信小程序，(`id_channel`=3, `key1`=小程序的openid, `key2`=小程序的unionid)。
> 3. `data1`、`data2`、`data3` 保留字段，用于不同的 channel 对应的会话数据字段，不索引。比如对于微信小程序，(`id_channel`=3, `data1`=session_key)。
> 4. 客户端和服务器经过身份验证后，就交由session来进行一般性会话。

| id_channel | key1 | key2 | key3 | data1 | data2 | data3
|----|----|----|----|----|----|----
| 小程序 3 | openid | unionid | | session_key | |