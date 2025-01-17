<template>
  <div>
    <Navbar />
    <h2 class="centered">User Information</h2>
    <p class="centered">Welcome to the User Info Page!</p>

    <!-- New section for displaying user data -->
    <div class="user-data">
      <!-- Dummy user image -->
      <img :src="user.image" alt="User Profile" class="user-image" />
      <h3 class="user-details-title">User Details</h3>
      <div class="user-details">
        <p><strong>Name:</strong> {{ user.name }}</p>
        <p><strong>Email:</strong> {{ user.email }}</p>
        <p><strong>Age:</strong> {{ user.age }}</p>
      </div>
    </div>

    <div class="button-group">
      <button @click="checkEligibility">Check Eligibility</button>
      <button @click="fillForm">Fill Up Form</button>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';
// Import the image directly
import userImage from '@/assets/image.gif';

export default {
  name: 'UserInfo',
  components: {
    Navbar
  },
  data() {
    return {
      // Sample user data with the imported image
      user: {
        name: 'John Doe',
        email: 'johndoe@example.com',
        age: 30,
        image: userImage // Use the imported image
      }
    };
  },
  methods: {
    checkEligibility() {
      this.$router.push({ name: 'CheckEligibility' }); // Make sure 'CheckEligibility' is defined in your router
    },
    fillForm() {
      this.$router.push({ name: 'FillForm' }); // Make sure 'FillForm' is defined in your router
    }
  }
}
</script>

<style scoped>
.centered {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
  font-family: Arial, sans-serif;
}

.user-data {
  margin-top: 20px;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin-left: auto;
  margin-right: auto;
  text-align: center; /* Keep the overall text alignment center for header and image */
}

.user-image {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 15px;
  border: 3px solid #007bff;
}

.user-details {
  text-align: left; /* Align the user details text to the left */
  margin-top: 10px;
}

.user-details-title {
  margin-bottom: 10px;
  font-size: 1.2rem;
}

.button-group {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-top: 20px;
}

button {
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  box-shadow: 0 3px 5px rgba(0, 0, 0, 0.2);
}

button:hover {
  background-color: #0056b3;
}

button:active {
  transform: translateY(2px);
  box-shadow: 0 2px 3px rgba(0, 0, 0, 0.2);
}
</style>
