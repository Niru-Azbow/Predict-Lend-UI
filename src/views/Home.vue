<template>
  <div class="homepage">
    <Navbar />
    <div class="content">
      <h1>Welcome to the Portal</h1>
      <p>Please choose your login option below:</p>
      <div class="home-buttons">
        <button @click="goToAdminLogin">Admin Login</button>
        <button @click="goToUserLoginPage">User Login</button>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';

export default {
  name: 'HomePage',
  components: {
    Navbar
  },
  methods: {
    goToAdminLogin() {
      this.$router.push({ name: 'AdminLogin' });
    },
    goToUserLoginPage() {
      this.$router.push({ name: 'UserLogin' });
    }
  }
}
</script>

<style scoped>
.homepage {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #f0f4f8 0%, #d9e8fc 100%);
  padding: 40px 20px;
  font-family: 'Arial', sans-serif;
}

.content {
  text-align: center;
  background-color: white;
  padding: 30px;
  margin-top: 120px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  max-width: 600px;
  width: 100%;
}

h1 {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
}

p {
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 30px;
}

.home-buttons {
  display: flex;
  justify-content: center;
  gap: 20px;
}

button {
  padding: 15px 30px;
  font-size: 16px;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 25px;
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s, transform 0.3s;
}

button:hover {
  background-color: #0056b3;
  transform: translateY(-5px);
}

button:focus {
  outline: none;
  box-shadow: 0px 0px 0px 3px rgba(0, 123, 255, 0.5);
}
</style>
