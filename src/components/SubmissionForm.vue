<template>
  <div class="page-wrapper">
    <div class="form-container">
      <img
        src="@/assets/c69a5462aa89e8f99915db243660f7f7c5478a6e.png"
        alt="GreenTech Logo"
        class="logo"
      />

      <form
        v-if="!showThankYou"
        @submit.prevent="handleSubmit"
        class="form-wrapper"
      >
        <h1 class="form-title">Have us reach out</h1>
        <div class="form-group" v-for="field in fields" :key="field.id">
          <label :for="field.id" class="label">{{ field.label }}</label>
          <input
            :id="field.id"
            v-model="form[field.model]"
            :type="field.type"
            :placeholder="field.placeholder || ''"
            required
          />
        </div>

        <button type="submit" :disabled="isSubmitting" class="submit-btn">
          Continue
        </button>
      </form>

      <div v-else class="thank-you">
        <div>Thank you</div>
        <div>We will contact you<br />shortly</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const API_KEY = "b6e569b7-30d1-4235-b5f4-02977b2a990e";
const API_URL = `https://dev-api-api.hiring-test.experientialpreview.com/api/lead/${API_KEY}`;

const form = ref({
  first: "",
  last: "",
  company: "",
  phone: "",
  email: "",
});

const fields = [
  { id: "first", label: "First Name", model: "first", type: "text" },
  { id: "last", label: "Last Name", model: "last", type: "text" },
  { id: "email", label: "Email", model: "email", type: "email" },
  { id: "phone", label: "Phone Number", model: "phone", type: "tel" },
  { id: "company", label: "Company", model: "company", type: "text" },
];

const showThankYou = ref(false);
const isSubmitting = ref(false);

async function handleSubmit() {
  isSubmitting.value = true;

  try {
    const res = await fetch(API_URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(form.value),
    });

    if (!res.ok) throw new Error("Failed to submit form.");

    showThankYou.value = true;

    setTimeout(() => {
      showThankYou.value = false;
      form.value = { first: "", last: "", company: "", phone: "", email: "" };
    }, 5000);
  } catch (err) {
    console.error("Error submitting form:", err);
    alert("Something went wrong. Please try again.");
  } finally {
    isSubmitting.value = false;
  }
}
</script>

<style scoped>
.page-wrapper {
  background-color: #f4f2ee;
  min-height: 100vh;
  min-width: 360px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.form-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  width: 100%;
  max-width: 393px;
  height: 852px;
  padding: 0 24px;
  position: relative;
}

.logo {
  width: 122.83px;
  height: 40px;
  position: absolute;
  top: 40px;
  left: 24px;
}

.form-title {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  font-size: 25px;
  line-height: 100%;
  color: #555552;
  margin-bottom: 5px;
}

.form-wrapper {
  width: 100%;
  max-width: 310px;
  max-height: 852px;
  display: flex;
  flex-direction: column;
  gap: 1.6rem;
  margin: 120px 0;
}

.form-group {
  position: relative;
  display: flex;
  flex-direction: column;
}

label {
  font-family: "ABeeZee", sans-serif;
  position: absolute;
  top: -7px;
  left: 12px;
  font-weight: 400;
  background-color: #f4f2ee;
  z-index: 100;
  font-size: 12px;
  line-height: 100%;
  color: #006315;
  padding: 0 5px;
}

input {
  width: 100%;
  max-width: 310px;
  height: 40.32px;
  border-radius: 3.6px;
  border: 0.72px solid #555552;
  background-color: #f4f2ee;
  box-sizing: border-box;
  box-shadow: none;
  font-family: "ABeeZee", sans-serif;
  font-size: 15px;
  color: #555552;
  padding: 10px 12px;
}

.submit-btn {
  width: 131px;
  max-width: 310px;
  height: 34.83px;
  border-radius: 4px;
  background-color: #0b476c;
  color: #ffffff;
  align-self: flex-end;
  border: none;
  font-family: "ABeeZee", sans-serif;
  cursor: pointer;
  margin-top: 20px;
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.thank-you {
  font-family: "Roboto", sans-serif;
  text-align: center;
  font-size: 25px;
  color: #555552;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>

<style>
html,
body {
  background-color: #f4f2ee;
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: sans-serif;
  box-sizing: border-box;
}
*,
*::before,
*::after {
  box-sizing: inherit;
}
</style>
