<template>
  <div>
    <Navbar />
    <h2>Add New User</h2>

    <!-- Form for adding a new user -->
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Name:</label>
        <input type="text" v-model="user.name" id="name" required />
      </div>

      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="user.email" id="email" required />
      </div>

      <div>
        <label for="age">Age:</label>
        <input type="number" v-model="user.age" id="age" required />
      </div>

      <button type="submit">Submit</button>
    </form>

    <!-- Display the user data after form submission -->
    <div v-if="submitted" class="user-data">
      <h3>User Details</h3>
      <p><strong>Name:</strong> {{ user.name }}</p>
      <p><strong>Email:</strong> {{ user.email }}</p>
      <p><strong>Age:</strong> {{ user.age }}</p>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';

export default {
  name: 'AddUser',
  components: {
    Navbar
  },
  data() {
    return {
      user: {
        name: '',
        email: '',
        age: null
      },
      submitted: false // To track whether the form has been submitted
    };
  },
  methods: {
    submitForm() {
      this.submitted = true; // Mark form as submitted
      // Here you can also send the user data to an API or perform other actions
    }
  }
}
</script>

<style scoped>
form {
  margin: 20px 0;
}

form div {
  margin-bottom: 10px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  padding: 5px;
  width: 100%;
  max-width: 300px;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.user-data {
  margin-top: 20px;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
}
</style>
