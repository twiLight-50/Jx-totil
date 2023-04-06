<template>
  <div class="detail-step">
    <JxSteps :active="order.orderState===6?1:order.orderState">
      <JxStepsItem title="提交订单" :desc="order.createTime"  />
      <JxStepsItem title="付款成功" :desc="order.payTime"  />
      <JxStepsItem title="商品发货" :desc="order.consignTime"  />
      <JxStepsItem title="确认收货" :desc="order.endTime"  />
      <JxStepsItem title="订单完成" :desc="order.evaluationTime"  />
    </JxSteps>
  </div>
</template>
<script>
export default {
  name: 'DetailStep',
  props: {
    order: {
      type: Object,
      default: () => ({})
    }
  }
}
</script>
<style scoped lang="less">
.detail-step {
  padding: 20px;
}
</style>
