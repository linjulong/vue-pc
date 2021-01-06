<template>
  <input type="text" placeholder="测试" @input="$emit('input', $event.target.value)" :value="value">
</template>

<script>
export default {
  props: {
    value: {
      type: String
    }
  }
}
</script>

<style>
</style>