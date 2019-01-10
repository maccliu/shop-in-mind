# 不使用AUTO_INCREMENT创建一个新用户id

```sql
INSERT INTO
    `bc_user` (`user_id`, `nickname`, `user_rank`)
SELECT
    CASE
        WHEN MAX(`user_id`) IS NULL
        THEN 1
        ELSE MAX(`user_id`) + 1
    END AS `new_user_id`,
    "张三",
    6
FROM
    `bc_user`
```