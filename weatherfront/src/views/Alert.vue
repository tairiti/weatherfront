<template>
  <div v-show="message != null && message.length > 0">
  {{message}}
  </div>
</template>
<script>
export default {
  name: 'Alert',
  props:{
    message: {}
  }
}
</script>