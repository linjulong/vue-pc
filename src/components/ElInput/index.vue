<template>
  <el-input :value="value" placeholder="请输入内容" v-bind="$attrs" v-on="inputListeners"></el-input>
</template>

<script>
export default {
  props: {
    value: {
      type: String
    }
  },
  computed: {
    inputListeners: function () {
      var vm = this
      return Object.assign({},
        // 我们从父级添加所有的监听器
        this.$listeners,
        // 然后我们添加自定义监听器，
        // 或覆写一些监听器的行为
        {
          // 这里确保组件配合 `v-model` 的工作
          input: function ($event) {
            // 默认会把整个event冒泡上去，也是v-model实现成功
            vm.$emit('input', $event)
          }
        }
      )
    }
  }
}
</script>

<style>
</style>