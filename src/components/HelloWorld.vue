<template>
  <div>{{ msg }}</div>
  <button @click="changeMsg">Change</button>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const msg = ref("hello")

    const changeMsg = () => {
      msg.value = "world"
    }

    return{
      msg,
      changeMsg
    }
  }
}
</script>