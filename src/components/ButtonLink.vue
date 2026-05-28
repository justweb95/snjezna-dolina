<script setup>
  const btnProps = defineProps({
    text: String,
    url: String,
    type: {
      type: String,
      default: 'primary',
        validator: (value) => ['primary', 'secondary'].includes(value),
    },
  });


</script>

<template>
  
</template>

<style lang="scss" scoped>

</style>