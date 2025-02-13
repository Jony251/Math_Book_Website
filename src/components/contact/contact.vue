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
          @blur="validateField('name')"
        >
        <p v-if="errors.name" class="error">{{ errors.name }}</p>
      </div>

      <div class="form-group">
        <input 
          type="tel" 
          id="phone" 
          v-model="formData.phone"
          required
          placeholder="Номер телефона"
          @blur="validateField('phone')"
        >
        <p v-if="errors.phone" class="error">{{ errors.phone }}</p>
      </div>

      <div class="form-group">
        <input 
          type="email" 
          id="email" 
          v-model="formData.email"
          required
          placeholder="Ваш email"
          @blur="validateField('email')"
        >
        <p v-if="errors.email" class="error">{{ errors.email }}</p>
      </div>

      <button type="submit" class="submit-btn" :disabled="!isFormValid || isSubmitting">
        {{ isSubmitting ? 'Отправка...' : 'Отправить' }}
      </button>
    </form>
    <div v-if="submitStatus.show" :class="['submit-status', submitStatus.type]">
      {{ submitStatus.message }}
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, computed } from 'vue'
import emailjs from '@emailjs/browser'
import './contact.css'

const EMAILJS_PUBLIC_KEY = import.meta.env.VITE_EMAILJS_PUBLIC_KEY
const EMAILJS_TEMPLATE_ID = import.meta.env.VITE_EMAILJS_TEMPLATE_ID
const EMAILJS_SERVICE_ID = import.meta.env.VITE_EMAILJS_SERVICE_ID

const formData = reactive({
  name: '',
  phone: '',
  email: '',
  date: new Date().toLocaleString()
})

const errors = reactive({
  name: '',
  phone: '',
  email: ''
})

const isSubmitting = ref(false)
const submitStatus = reactive({
  show: false,
  message: '',
  type: 'success'
})

const validateField = (field) => {
  switch (field) {
    case 'name':
      errors.name = !formData.name.trim() 
        ? 'Имя обязательно' 
        : formData.name.length < 2 
          ? 'Имя должно быть минимум 2 символа' 
          : ''
      break
    case 'phone':
      const phoneRegex = /^(\+)?[\d\s-]{10,}$/
      errors.phone = !formData.phone.trim() 
        ? 'Телефон обязателен' 
        : !phoneRegex.test(formData.phone) 
          ? 'Введите корректный номер телефона' 
          : ''
      break
    case 'email':
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      errors.email = !formData.email.trim() 
        ? 'Email обязателен' 
        : !emailRegex.test(formData.email) 
          ? 'Введите корректный email адрес' 
          : ''
      break
  }
}

const validateForm = () => {
  validateField('name')
  validateField('phone')
  validateField('email')
}

const isFormValid = computed(() => {
  return formData.name && 
         formData.phone && 
         formData.email && 
         !errors.name && 
         !errors.phone && 
         !errors.email
})

const showStatus = (message, type = 'success') => {
  submitStatus.show = true
  submitStatus.message = message
  submitStatus.type = type
  setTimeout(() => {
    submitStatus.show = false
  }, 5000)
}

const handleSubmit = async () => {
  validateForm()
  
  if (!isFormValid.value) {
    showStatus('Пожалуйста, исправьте ошибки в форме', 'error')
    return
  }

  isSubmitting.value = true
  
  try {
    const response = await emailjs.send(
      EMAILJS_SERVICE_ID,
      EMAILJS_TEMPLATE_ID,
      {
        name: formData.name,
        email: formData.email,
        phone: formData.phone,
        date: formData.date,
        message: `Новая заявка от клиента:
        
Имя: ${formData.name}
Телефон: ${formData.phone}
Email: ${formData.email}
Дата: ${formData.date}`
      },
      EMAILJS_PUBLIC_KEY
    )

    if (response.status === 200) {
      showStatus('Сообщение успешно отправлено!')
      // Reset form
      formData.name = ''
      formData.phone = ''
      formData.email = ''
    } else {
      throw new Error('Failed to send email')
    }
  } catch (error) {
    console.error('Email sending error:', error)
    showStatus('Произошла ошибка при отправке. Пожалуйста, попробуйте позже.', 'error')
  } finally {
    isSubmitting.value = false
  }
}
</script>