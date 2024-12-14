<script setup lang="ts">
import { useCountryStore } from '@/stores/country'
import { storeToRefs } from 'pinia'
import { ref, onMounted } from 'vue'
const { countryList } = storeToRefs(useCountryStore())
const submitForm = () => {
  const { selectedOption, inputField } = formData.value

  if (selectedOption && inputField) {
    localStorage.setItem('selectedOption', selectedOption)

    const country = countryList.value.find((country) => country.code === selectedOption)
    const finalPhoneNumber = country ? `${country.dial_code}${inputField}` : inputField

    const whatsappUrl = `https://wa.me/${finalPhoneNumber}`
    window.open(whatsappUrl, '_blank')
  } else {
    alert('Please select a country and enter a phone number')
  }
}

const resetForm = () => {
  formData.value = {
    selectedOption: '',
    inputField: '',
  }
  localStorage.removeItem('selectedOption')
}

const saveOption = (option: string) => {
  localStorage.setItem('selectedOption', option)
}
const formData = ref({
  selectedOption: '',
  inputField: '',
})

onMounted(() => {
  const storedOption = localStorage.getItem('selectedOption') || 'NP'
  const selectedCountry = countryList.value.find((country) => country.code === storedOption)
  formData.value.selectedOption = selectedCountry ? selectedCountry.code : 'NP'
})
</script>

<template>
  <div class="form-container">
    <h2 class="form-title">Add any phone number to whatsapp</h2>
    <form class="form" @submit.prevent="submitForm">
      <div class="form-group">
        <label for="select" class="form-label">Select a Country:</label>
        <select
          v-model="formData.selectedOption"
          @change="saveOption(formData.selectedOption)"
          id="select"
          class="form-select"
          required
        >
          <option value="" disabled>Select a country</option>
          <option v-for="option in countryList" :key="option.code" :value="option.code">
            {{ option.name }}
          </option>
        </select>
      </div>
      <div class="form-group">
        <label for="input" class="form-label">Phone Number:</label>
        <input
          type="text"
          v-model="formData.inputField"
          id="input"
          class="form-input"
          placeholder="Enter details here"
          required
        />
      </div>
      <div class="form-actions">
        <button type="submit" class="form-button submit">Submit</button>
        <button type="button" class="form-button reset" @click="resetForm">Reset</button>
      </div>
    </form>
  </div>
</template>

<style>
/* Container styles */
.form-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  font-family: Arial, sans-serif;
}

/* Title styles */
.form-title {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

/* Form group styles */
.form-group {
  margin-bottom: 15px;
}

/* Label styles */
.form-label {
  display: block;
  font-weight: bold;
  margin-bottom: 5px;
  color: #555;
}

/* Select styles */
.form-select {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
}

/* Input styles */
.form-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
}

/* Button styles */
.form-actions {
  display: flex;
  justify-content: space-between;
}

.form-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}

.form-button.submit {
  background-color: #4caf50;
  color: white;
}

.form-button.submit:hover {
  background-color: #45a049;
}

.form-button.reset {
  background-color: #f44336;
  color: white;
}

.form-button.reset:hover {
  background-color: #e53935;
}
</style>
