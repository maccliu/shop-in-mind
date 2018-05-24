# 数据设计

## 系统配置

| 表 | 说明
|----|----
| [bc_user_rank](bc_user_rank.md) | 用户级别设置
| [bc_warehouse](bc_warehouse.md) | 仓库设置
| [bc_currency_rate](bc_currency_rate.md) | 汇率设置
| [bc_delivery_mode](bc_delivery_mode.md) | 快递模板

## 用户

| 表 | 说明
|----|----
| [bc_user](bc_user.md) | 用户主表
| [bc_user_account](bc_user_account.md) | 用户登录账号
| [bc_user_safe_question](bc_user_safe_question.md) | 用户安全问题

## 商品

| 表 | 说明
|----|----
| [bc_spu](bc_user.md) | 商品主表
| [bc_spu_price](bc_spu_price.md) | 商品价格表
| [bc_spu_price_view](bc_spu_price_view.md) | 商品价格视图

## 购物车

| 表 | 说明
|----|----
| [bc_cart](bc_cart.md) | 购物车主表
| [bc_cart_item](bc_cart_item.md) | 购物车商品

## 订单

| 表 | 说明
|----|----
| [bc_order](bc_cart.md) | 订单主表
| [bc_order_item](bc_cart_item.md) | 订单商品
| [bc_order_adjustment](bc_order_adjustment.md) | 订单调价记录
| [bc_order_payment](bc_order_payment.md) | 订单支付记录
| [bc_order_service](bc_order_service.md) | 订单售后记录

## CMS

| 表 | 说明
|----|----
| [bc_cms_block](bc_cms_block.md) | 展示区块