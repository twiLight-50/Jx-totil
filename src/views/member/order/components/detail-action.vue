<template>
  <div class="detail-action">
    <div class="state">
      <span class="iconfont icon-order-unpay"></span>
      <p>{{orderStatus[order.orderState].label}}</p>
    </div>
    <div class="info">
      <p>订单编号：{{order.id}}</p>
      <p>下单时间：{{order.createTime}}</p>
    </div>
    <div class="btn">
      <!-- 待付款 -->
      <template v-if="order.orderState === 1">
        <JxButton @click="$router.push('/member/pay?id='+order.id)" type="primary" size="small">立即付款</JxButton>
        <JxButton @click="handlerCancel(order)" type="gray" size="small">取消订单</JxButton>
      </template>
      <!-- 待发货 -->
      <template v-if="order.orderState === 2">
        <JxButton @click="$router.push(`/member/checkout?orderId=${order.id}`)" type="primary" size="small">再次购买</JxButton>
      </template>
      <!-- 待收货 -->
      <template v-if="order.orderState === 3">
        <JxButton @click="handlerConfirm(order)" type="primary" size="small">确认收货</JxButton>
        <JxButton  @click="$router.push(`/member/checkout?orderId=${order.id}`)" type="plain" size="small">再次购买</JxButton>
      </template>
      <!-- 待评价 -->
      <template v-if="order.orderState === 4">
        <JxButton  @click="$router.push(`/member/checkout?orderId=${order.id}`)" type="primary" size="small">再次购买</JxButton>
        <JxButton type="plain" size="small">评价商品</JxButton>
        <JxButton type="gray" size="small">申请售后</JxButton>
      </template>
      <!-- 已完成 -->
      <template v-if="order.orderState === 5">
        <JxButton  @click="$router.push(`/member/checkout?orderId=${order.id}`)" type="primary" size="small">再次购买</JxButton>
        <JxButton type="plain" size="small">查看评价</JxButton>
        <JxButton type="gray" size="small">申请售后</JxButton>
      </template>
      <!-- 已取消 -->
    </div>
    <Teleport to="#model">
      <OrderCancel ref="orderCancelCom"/>
    </Teleport>
  </div>
</template>
<script>
import { orderStatus } from '@/api/constants'
import OrderCancel from './order-cancel'
import { useCancel, useConfirm } from '../index'
export default {
  name: 'OrderDetailAction',
  props: {
    order: {
      type: Object,
      default: () => ({})
    }
  },
  components: {
    OrderCancel
  },
  setup () {
    return { orderStatus, ...useCancel(), ...useConfirm() }
  }
}
</script>
<style scoped lang="less">
.detail-action {
  height: 180px;
  width: 100%;
  display: flex;
  align-items: center;
  .state {
    width: 220px;
    text-align: center;
    .iconfont {
      font-size: 40px;
      color: @JxColor;
    }
    p {
      font-size: 16px;
      color: #666;
      margin-bottom: 10px;
    }
  }
  .info {
    width: 240px;
    line-height: 30px;
    p {
      color: #999;
    }
  }
  .btn {
    flex: 1;
    text-align: right;
    margin-right: 100px;
    .Jx-button {
      margin-left: 20px;
    }
  }
}
</style>
