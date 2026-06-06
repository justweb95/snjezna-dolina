<script setup>
  const btnProps = defineProps({
    text: String,
    action: String,
    type: {
      type: String,
      default: 'primary',
      validator: (value) => ['primary', 'secondary', 'button-phone'].includes(value),
    },
  });

  import buttonIcon from '../assets/images/home/button-icon.svg';
  import buttonIconWhite from '../assets/images/home/button-icon-white.svg';
  
  import buttonPhoneIcon from '../assets/images/home/phone-icon.svg';

</script>

<template>
  <a
    :href="btnProps.action"
    :class="[
      'btn',
      btnProps.type === 'button-phone' ? 'primary' : btnProps.type,
      { 'button-phone': btnProps.type === 'button-phone' },
    ]"
  >
    <img
     :src="btnProps.type === 'button-phone' ? buttonPhoneIcon : (btnProps.type === 'primary' ? buttonIcon : buttonIconWhite)" 
     class="button-icon"
     :alt="btnProps.type === 'button-phone' ? 'Phone button icon' : 'Button icon'" />
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
    background-color: #101C2A;
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

  &.button-phone {
    .button-icon {
      padding: 0;
    }
  }
  
  &.secondary {
    margin: 40px auto 0;
    background-color: #fff;
    color: #101C2A;

    .button-icon {
      background-color: #101C2A;
    }
    
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

@media (max-width: 550px) {
  .btn.button-phone {
    width: 56px;
    height: 56px;
    padding: 0;
    border-radius: 50%;

    .btn-text {
      display: none;
    }

    .button-icon {
      position: static;
      left: auto;
      top: auto;
      transform: none;
    }

    &:hover .button-icon {
      left: auto;
      transform: none;
    }

    &:hover .btn-text {
      transform: none;
    }
  }
}

</style>