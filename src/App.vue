<script>
import RegisterForm from './components/RegisterForm.vue'

export default {
  components: {
    RegisterForm
  }
}
</script>

<template>
  <div class="content">
    <RegisterForm />
  </div>
</template>

<style scoped>
  .content {
    display:flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100vw;
    height: 100vh;
  }
</style>


