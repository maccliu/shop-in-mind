# bc_user_safe_question 基本表

用户的密码安全问题。

## SQL定义

```sql

DROP TABLE IF EXISTS `bc_user_safe_question`;

CREATE TABLE `bc_user_safe_question` (
  `user_id` int(11) NOT NULL,
  `sq_salt` varchar(10) DEFAULT '' COMMENT '专用salt',
  `safe_question1` varchar(127) DEFAULT NULL COMMENT '安全问题1',
  `safe_answer1` varchar(63) DEFAULT NULL COMMENT '安全答案1，明文',
  `safe_hash1` varchar(32) DEFAULT NULL COMMENT '安全答案1，hash',
  `safe_question2` varchar(127) DEFAULT NULL COMMENT '安全问题2',
  `safe_answer2` varchar(63) DEFAULT NULL COMMENT '安全答案2，明文',
  `safe_hash2` varchar(32) DEFAULT NULL COMMENT '安全答案2，hash',
  `safe_question3` varchar(127) DEFAULT NULL COMMENT '安全问题3',
  `safe_answer3` varchar(63) DEFAULT NULL COMMENT '安全答案3，明文',
  `safe_hash3` varchar(32) DEFAULT NULL COMMENT '安全答案3，hash',
  `updated_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户的密码安全问题';

```

> 备注：
> 1. `sq_salt`是密码安全问题的专用salt，一般不要和`bc_user_account`.`salt`一样，以免安全风险。
