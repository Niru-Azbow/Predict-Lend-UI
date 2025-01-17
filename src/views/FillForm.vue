<template>
  <form @submit.prevent="submitForm" class="loan-form">
    <!-- Personal Details Section -->
    <h2>Personal Details</h2>
    <fieldset>
      <legend>Primary Applicant</legend>
      <label for="fullName">Full Name</label>
      <input id="fullName" v-model="form.primaryApplicant.fullName" placeholder="Enter your full name" required />

      <label for="dob">Date of Birth</label>
      <input id="dob" v-model="form.primaryApplicant.dob" type="date" required />

      <label for="nic">NIC Number</label>
      <input id="nic" v-model="form.primaryApplicant.nic" placeholder="Enter your NIC" required />

      <label for="residenceAddress">Residence Address</label>
      <input id="residenceAddress" v-model="form.primaryApplicant.residenceAddress" placeholder="Your current residence address" required />

      <label for="correspondenceAddress">Correspondence Address (Optional)</label>
      <input id="correspondenceAddress" v-model="form.primaryApplicant.correspondenceAddress" placeholder="Enter if different from residence" />

      <!-- Duration of Stay at Present Address -->
      <label>Duration of Stay at Present Address</label>
      <div class="duration-of-stay">
        <input v-model="form.primaryApplicant.durationYears" type="number" placeholder="Years" required />
        <input v-model="form.primaryApplicant.durationMonths" type="number" placeholder="Months" required />
      </div>
      <!-- No.of dependents -->
      <label for="No.ofdependants">Number of dependants</label>
      <input id="No.ofdependants" v-model="form.primaryApplicant.dependants" type="number" placeholder="Enter number of dependants" />
      <!-- Type of Residence -->
      <label>Type of Residence</label>
      <div>
        <label><input type="radio" v-model="form.primaryApplicant.residenceType" value="Owned" /> Owned</label>
        <label><input type="radio" v-model="form.primaryApplicant.residenceType" value="Rented" /> Rented</label>
        <label><input type="radio" v-model="form.primaryApplicant.residenceType" value="With Parents" /> With Parents</label>
        <label><input type="radio" v-model="form.primaryApplicant.residenceType" value="Other" /> Other</label>
      </div>

      <label for="phone">Phone</label>
      <input id="phone" v-model="form.primaryApplicant.phone" placeholder="Enter your phone number" required />

      <label for="email">Email</label>
      <input id="email" v-model="form.primaryApplicant.email" type="email" placeholder="Your email address" required />

      <!-- Marital Status -->
      <label>Marital Status</label>
      <div>
        <label><input type="radio" v-model="form.primaryApplicant.maritalStatus" value="Single" /> Single</label>
        <label><input type="radio" v-model="form.primaryApplicant.maritalStatus" value="Married" /> Married</label>
        <label><input type="radio" v-model="form.primaryApplicant.maritalStatus" value="Divorced" /> Divorced</label>
      </div>

      <!-- Gender -->
      <label>Gender</label>
      <div>
        <label><input type="radio" v-model="form.primaryApplicant.gender" value="Male" /> Male</label>
        <label><input type="radio" v-model="form.primaryApplicant.gender" value="Female" /> Female</label>
        <label><input type="radio" v-model="form.primaryApplicant.gender" value="Other" /> Other</label>
      </div>


          <!-- Educational Status -->
      <label>Educational Status</label>
      <div>
        <label><input type="radio" v-model="form.primaryApplicant.educationalstatus" value="Primary" /> Primary</label>
        <label><input type="radio" v-model="form.primaryApplicant.educationalstatus" value="Secondary" /> Secondary</label>
        <label><input type="radio" v-model="form.primaryApplicant.educationalstatus" value="Diploma" /> Diploma</label>
        <label><input type="radio" v-model="form.primaryApplicant.educationalstatus" value="Graduate" /> Graduate</label>
        <label><input type="radio" v-model="form.primaryApplicant.educationalstatus" value="Post-Graduate" /> Post-Graduate</label>
        <label><input type="radio" v-model="form.primaryApplicant.educationalstatus" value="Professionals(CIMA/CA)" /> Professionals(CIMA/CA)</label>
      </div>
    </fieldset>
    <!-- Joint Applicant Section -->
    <fieldset v-if="form.hasJointApplicant">
      <legend>Joint Applicant (Spouse)</legend>
      <label for="jointFullName">Full Name</label>
      <input id="jointFullName" v-model="form.jointApplicant.fullName" placeholder="Spouse's full name" />

      <label for="jointDob">Date of Birth</label>
      <input id="jointDob" v-model="form.jointApplicant.dob" type="date" />

      <label for="jointNic">NIC Number</label>
      <input id="jointNic" v-model="form.jointApplicant.nic" placeholder="Spouse's NIC" />

      <label for="jointEmploymentStatus">Employment Status</label>
      <select id="jointEmploymentStatus" v-model="form.jointApplicant.employmentStatus">
        <option value="">Select employment status</option>
        <option>Permanent</option>
        <option>Contract</option>
      </select>

      <label for="jointPhone">Phone</label>
      <input id="jointPhone" v-model="form.jointApplicant.phone" placeholder="Spouse's phone number" />

      <label for="jointEmail">Email</label>
      <input id="jointEmail" v-model="form.jointApplicant.email" type="email" placeholder="Spouse's email address" />
    </fieldset>

    <button type="button" @click="toggleJointApplicant" class="toggle-btn">
      {{ form.hasJointApplicant ? 'Remove Joint Applicant' : 'Add Joint Applicant' }}
    </button>

    <!-- Employment Details Section -->
    <h2>Employment Details</h2>
    <fieldset>
      <label for="employmentStatus">Employment Status</label>
      <select id="employmentStatus" v-model="form.primaryApplicant.employmentStatus" required>
        <option value="">Select employment status</option>
        <option>Employed</option>
        <option>Self-employed</option>
        <option>Unemployed</option>
      </select>

      <label for="jobTitle">Job Title</label>
      <input id="jobTitle" v-model="form.primaryApplicant.jobTitle" placeholder="Your job title" />

      <label for="employer">Employer</label>
      <input id="employer" v-model="form.primaryApplicant.employer" placeholder="Name of employer" />

      <label for="employmentYears">Years at Current Job</label>
      <input id="employmentYears" v-model="form.primaryApplicant.employmentYears" type="number" placeholder="Years" />

      <label for="employmentMonths">Months at Current Job</label>
      <input id="employmentMonths" v-model="form.primaryApplicant.employmentMonths" type="number" placeholder="Months" />
    </fieldset>

    <!-- Income Details Section -->
    <h2>Income Details</h2>
    <fieldset>
      <label for="monthlyIncome">Monthly Income (in Rupees)</label>
      <input id="monthlyIncome" v-model="form.primaryApplicant.monthlyIncome" type="number" placeholder="Enter your monthly income" required />

      <label for="otherIncome">Other Income (if any)</label>
      <input id="otherIncome" v-model="form.primaryApplicant.otherIncome" type="number" placeholder="Enter other income" />

      <label for="totalIncome">Total Income</label>
      <input id="totalIncome" :value="totalIncome" type="number" readonly />
    </fieldset>

    <!-- Expenses Details Section -->
    <h2>Expenses Details</h2>
    <fieldset>
      <label for="rentOrMortgage">Monthly Rent/Mortgage</label>
      <input id="rentOrMortgage" v-model="form.expenses.rentOrMortgage" type="number" placeholder="Enter monthly rent or mortgage" required />

      <label for="utilities">Utilities (Electricity, Water, etc.)</label>
      <input id="utilities" v-model="form.expenses.utilities" type="number" placeholder="Enter monthly utilities expenses" />

      <label for="groceries">Groceries</label>
      <input id="groceries" v-model="form.expenses.groceries" type="number" placeholder="Enter monthly groceries expenses" />

      <label for="transportation">Transportation</label>
      <input id="transportation" v-model="form.expenses.transportation" type="number" placeholder="Enter monthly transportation expenses" />

      <label for="otherExpenses">Other Expenses</label>
      <input id="otherExpenses" v-model="form.expenses.otherExpenses" type="number" placeholder="Enter other monthly expenses" />

      <label for="totalExpenses">Total Expenses</label>
      <input id="totalExpenses" :value="totalExpenses" type="number" readonly />
    </fieldset>

    <!-- Loan Details Section -->
    <h2>Loan Details</h2>
    <fieldset>
      <label for="loanAmount">Loan Amount</label>
      <input id="loanAmount" v-model="form.loan.loanAmount" type="number" placeholder="Enter loan amount" required />

      <label for="loanTerm">Loan Term (Years)</label>
      <input id="loanTerm" v-model="form.loan.loanTerm" type="number" placeholder="Enter loan term in years" required />

      <label for="loanPurpose">Loan Purpose</label>
      <input id="loanPurpose" v-model="form.loan.loanPurpose" placeholder="Enter loan purpose" required />
    </fieldset>

    <!-- Submit Button -->
    <div v-if="submitStatus">
      <p :class="submitStatus.type">{{ submitStatus.message }}</p>
    </div>
    <button type="submit" class="submit-btn">Submit Application</button>
  </form>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      form: {
        primaryApplicant: {
          fullName: '',
          dob: '',
          nic: '',
          residenceAddress: '',
          correspondenceAddress: '',
          durationYears: null,
          durationMonths: null,
          dependants: null,
          residenceType: '',
          phone: '',
          email: '',
          maritalStatus: '',
          gender: '',
          educationalstatus: '',
          employmentStatus: '',
          jobTitle: '',
          employer: '',
          employmentYears: null,
          employmentMonths: null,
          monthlyIncome: null,
          otherIncome: null,
        },
        jointApplicant: {
          fullName: '',
          dob: '',
          nic: '',
          employmentStatus: '',
          phone: '',
          email: '',
        },
        hasJointApplicant: false,
        expenses: {
          rentOrMortgage: null,
          utilities: null,
          groceries: null,
          transportation: null,
          otherExpenses: null,
        },
        loan: {
          loanAmount: null,
          loanTerm: null,
          loanPurpose: '',
        },
      },
      submitStatus: null,
    };
  },
  computed: {
    totalIncome() {
      return this.form.primaryApplicant.monthlyIncome + (this.form.primaryApplicant.otherIncome || 0);
    },
    totalExpenses() {
      return this.form.expenses.rentOrMortgage + (this.form.expenses.utilities || 0) + (this.form.expenses.groceries || 0) +
        (this.form.expenses.transportation || 0) + (this.form.expenses.otherExpenses || 0);
    },
  },
  methods: {
    toggleJointApplicant() {
      this.form.hasJointApplicant = !this.form.hasJointApplicant;
    },
    async submitForm() {
      if (!this.form.primaryApplicant.fullName || !this.form.primaryApplicant.dob) {
        alert('Please fill in all required fields.');
        return;
      }

      try {
        const response = await axios.post('/api/loan-application', this.form);
        this.submitStatus = { type: 'success', message: 'Form submitted successfully!' };
        console.log('Form submitted successfully:', response.data);
      } catch (error) {
        this.submitStatus = { type: 'error', message: 'Error submitting the form. Please try again.' };
        console.error('Error submitting form:', error);
      }
    },
  },
};
</script>

<style scoped>
/* Add your CSS styles for the form here */
.loan-form {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
fieldset {
  border: 1px solid #ddd;
  padding: 10px;
  margin-bottom: 20px;
}
legend {
  font-weight: bold;
  font-size: 1.2em;
}
label {
  display: block;
  margin: 5px 0;
}
input,
select {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}
button {
  padding: 10px 20px;
  font-size: 1em;
  cursor: pointer;
}
.submit-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  width: 100%;
}
.submit-btn:hover {
  background-color: #45a049;
}
</style>




<style scoped>
.loan-form {
  max-width: 600px;
  margin: auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.loan-form h2 {
  text-align: center;
  color: #333;
}

fieldset {
  margin-bottom: 20px;
  border: 1px solid #ccc;
  padding: 10px 20px;
  border-radius: 5px;
}

legend {
  padding: 0 10px;
  font-weight: bold;
}

label {
  display: block;
  margin-top: 10px;
  color: #555;
}

input[type="text"],
input[type="date"],
input[type="number"],
input[type="email"],
select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.duration-of-stay {
  display: flex;
  gap: 10px;
}

.toggle-btn, .submit-btn {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  margin-top: 20px;
  cursor: pointer;
  font-size: 16px;
}

.toggle-btn:hover, .submit-btn:hover {
  background-color: #0056b3;
}

input[type="radio"] {
  margin-right: 5px;
}
</style>
<style scoped>
.loan-form {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  font-family: 'Arial', sans-serif;
}

h2 {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
}

.section {
  margin-bottom: 30px;
  padding: 15px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background-color: #fff;
}

.input-group {
  margin-bottom: 15px;
}

.input-group label {
  font-weight: bold;
  margin-bottom: 5px;
  display: block;
  color: #555;
}

.input-group input,
.input-group select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  color: #333;
}

.input-group input:focus,
.input-group select:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.radio-group {
  display: flex;
  gap: 15px;
  margin-top: 10px;
}

.radio-group label {
  font-size: 16px;
  color: #333;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #0056b3;
}

.toggle-btn {
  background-color: #6c757d;
  margin-bottom: 20px;
}

.submit-btn {
  width: 100%;
  background-color: #28a745;
}

.submit-btn:hover {
  background-color: #218838;
}
</style>
