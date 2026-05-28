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
  position: relative;
  display: flex;
  width: fit-content;
  align-items: center;
  justify-content: center;

  padding: 18px 36px 18px 12px;
  border-radius: 999px;

  font-weight: 600;
  text-decoration: none;

  overflow: hidden;

  transition:
    background-color .7s ease,
    color .3s ease;

  .btn-text {
    padding-left: 70px;

    transition:
      transform .7s cubic-bezier(0.22, 1, 0.36, 1);
  }

  .button-icon {
    position: absolute;
    left: 4px;
    top: 50%;

    transform: translateY(-50%);

    border-radius: 50%;
    background-color: #fff;
    padding: 14px 18px;

    transition:
      left .7s cubic-bezier(0.22, 1, 0.36, 1),
      transform .7s cubic-bezier(0.22, 1, 0.36, 1);
  }

  &.primary {
    margin: 40px auto 0;
    background-color: #13202E;
    color: #fff;

    &:hover {
      background-color: #2FB6EF;
      color: #fff;
    }

    /* ICON moves to far right */
    &:hover .button-icon {
      left: calc(100% - 6px);
      transform: translate(-100%, -50%) rotate(360deg);
    }

    /* TEXT moves left */
    &:hover .btn-text {
      transform: translateX(-40px);
    }
  }
}

</style>