<template>
  <div class="phone-button" @click="handleClick">
    <div class="phone-left">
      <img src="/images/phonecall.png" alt="позвонить">     
    </div>
    <div class="phone-right">
      <div class="phone-small">Заказать книгу</div>  
      <div class="phone-big">{{ formattedPhoneNumber }}</div>   
    </div>
  </div>
</template>

<script setup>
const phoneNumber = '0558858231'
const formattedPhoneNumber = '055-885-8231'

const handleClick = () => {
  // Add any click tracking logic here
  console.log('Phone button clicked')
  window.location.href = `tel:${phoneNumber}`
}
</script>

<style scoped>
@import './1_call_btn.css';
</style>



