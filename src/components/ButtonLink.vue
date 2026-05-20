<script setup>
  const btnProps = defineProps({
    text: String,
    url: String,
    type: {
      type: String,
      default: 'primary',
      validator: (value: string) => ['primary', 'secondary'].includes(value),
    },
  });


</script>

<template>
  
</template>

<style lang="scss" scoped>

</style>