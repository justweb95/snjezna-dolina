<script setup>
  const btnProps = defineProps({
    text: String,
    action: String,
    type: {
      type: String,
      default: 'primary',
      validator: (value) => ['primary', 'secondary'].includes(value),
    },
  });

  import buttonIcon from '../assets/images/home/button-icon.svg';
  import buttonIconWhite from '../assets/images/home/button-icon-white.svg';


</script>

<template>
  <a :href="btnProps.action" :class="['btn', btnProps.type]">
    <img
     :src="btnProps.type === 'primary' ? buttonIcon : buttonIconWhite" 
     class="button-icon"
     alt="Button icon" />
    <span class="btn-text">{{ btnProps.text }}</span>
  </a>
</template>

<style scoped>  

.btn {
  display: flex;
  width: fit-content;
  align-items: center;
  gap: 24px;

  padding: 4px 36px 4px 4px;
  border-radius: 999px;

  font-weight: 600;
  text-decoration: none;

  transition: background-color .7s ease, color 0.3s ease;

  .btn-text {
    transition: transform .7s cubic-bezier(0.22, 1, 0.36, 1);
  }

  .button-icon {
    border-radius: 50%;
    background-color: #fff;
    padding: 14px 18px;

    transition: transform .7s cubic-bezier(0.22, 1, 0.36, 1);
  }

  &.primary {
    margin: 40px auto 0;
    background-color: #13202E;
    color: #fff;

    &:hover {
      background-color: #2FB6EF;
      color: #fff;
    }

    /* ICON goes right */
    &:hover .button-icon {
      transform: translateX(222px) rotate(360deg);
    }

    /* TEXT moves left */
    &:hover .btn-text {
      transform: translateX(-50px);
    }
  }
}
  
</style>