<script setup>

  const emit = defineEmits(['get-massage'])

  const sendMsg = () =>{
    emit('get-massage','this is son msg')
  }


</script>

<template>
    <button @click="sendMsg">SON</button>
</template>

<style scoped>

</style>