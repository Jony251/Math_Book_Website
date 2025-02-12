import './contact.css'

<template>
  <div class="contact-container">
    <h1>Связаться с нами</h1>
    <form @submit.prevent="handleSubmit" class="contact-form">
      <div class="form-group">
        <input 
          type="text" 
          id="name" 
          v-model="formData.name"
          required
          placeholder="Ваше имя"
        >
      </div>

      <div class="form-group">
        <input 
          type="tel" 
          id="phone" 
          v-model="formData.phone"
          required
          placeholder="Номер телефона"
        >
      </div>

      <div class="form-group">
        <input 
          type="email" 
          id="email" 
          v-model="formData.email"
          required
          placeholder="Ваш email"
        >
      </div>

      <button type="submit" class="submit-btn">Отправить</button>
    </form>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import './contact.css'

const formData = reactive({
  name: '',
  phone: '',
  email: ''
})

const handleSubmit = () => {
  // Here you can add the logic to handle form submission
  console.log('Form submitted:', formData)
  // Reset form after submission
  formData.name = ''
  formData.phone = ''
  formData.email = ''
}
</script>