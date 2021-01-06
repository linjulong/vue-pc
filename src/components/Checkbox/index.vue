<template>
  <input type="checkbox" @change="$emit('change', $event.target.checked)" :checked="checked">
</template>

<script>
export default {
  props: {
    checked: {
      type: Boolean
    }
  },
  //组件中修改 v-model 指令，指定 prop 和 event
  model: {
    prop: 'checked',
    event: 'change'
  }
}
</script>

<style>
</style>