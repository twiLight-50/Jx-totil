<template>
  <div class="Jx-tabs-panel" v-show="name===activeName">
    <slot />
  </div>
</template>
<script>
import { inject } from 'vue'
export default {
  name: 'JxTabsPanel',
  // label 选项卡文字  name 选项卡唯一标识  div class="Jx-tabs-panel" 内容
  props: {
    label: {
      type: String,
      default: ''
    },
    name: {
      type: [String, Number],
      default: ''
    }
  },
  setup () {
    const activeName = inject('activeName')
    return { activeName }
  }
}
</script>
