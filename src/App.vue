<script setup>
import Contact from './components/contact/contact.vue'
import CallButton from './components/buttons/call_btn.vue'
import Header from './components/header/header.vue'
import Main from './components/main/main.vue'
import Footer from './components/footer/footer.vue'
</script>

<template>
  <div class="app-container">
    <header class="app-header">
      <Header />
    </header>
    <main class="main-content">
      <Main />
      <Contact />
      <CallButton />
    </main>
    <Footer />
  </div>
</template>
