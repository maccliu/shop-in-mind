# 不使用AUTO_INCREMENT创建一个新用户id

```sql
INSERT INTO
    `bc_user` (`id_user`, `nickname`, `user_rank`)
SELECT
    CASE
        WHEN MAX(`id_user`) IS NULL
        THEN 1
        ELSE MAX(`id_user`) + 1
    END AS `new_id_user`,
    "张三",
    6
FROM
    `bc_user`
```