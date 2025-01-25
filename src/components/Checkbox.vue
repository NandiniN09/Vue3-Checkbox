// App.vue
<template>
  <div class="form-container">
    <h1>Checkbox Design Functionality</h1>
    <div class="checkbox-group">
      <label v-for="option in options" :key="option.id" class="checkbox-label">
        <input
          type="checkbox"
          :value="option.id"
          v-model="selectedOptions"
          @change="handleCheckboxChange"
        />
        <span class="custom-checkbox"></span>
        {{ option.label }}
      </label>
    </div>
    <button :disabled="!canSave" class="save-button" @click="saveForm">
      Save
    </button>
  </div>
</template>

<script>
export default {
  name: 'CheckboxForm',
  data() {
    return {
      options: [
        { id: 1, label: 'Option 1' },
        { id: 2, label: 'Option 2' },
        { id: 3, label: 'Option 3' },
      ],
      selectedOptions:
        JSON.parse(localStorage.getItem('selectedOptions')) || [],
      canSave: false,
    };
  },
  watch: {
    selectedOptions: {
      handler(newVal) {
        this.canSave = newVal.length > 0;
        localStorage.setItem('selectedOptions', JSON.stringify(newVal));
      },
      deep: true,
    },
  },
  methods: {
    handleCheckboxChange() {
      // Logic to handle checkbox change is included in watcher
    },
    saveForm() {
      this.$toast.success('Form saved successfully!');
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

.form-container {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  background-color: #fdfdfd;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  font-family: 'Roboto', sans-serif;
  text-align: center;
}

h1 {
  font-size: 28px;
  color: #2c3e50;
  margin-bottom: 20px;
}

.checkbox-group {
  margin: 20px 0;
}

.checkbox-label {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  font-size: 16px;
  color: #34495e;
  cursor: pointer;
  position: relative;
  padding-left: 30px;
}

input[type='checkbox'] {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

.custom-checkbox {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #fff;
  border: 2px solid #3498db;
  border-radius: 4px;
  transition: all 0.3s ease;
}

input[type='checkbox']:checked ~ .custom-checkbox {
  background-color: #3498db;
  border-color: #2980b9;
}

input[type='checkbox']:checked ~ .custom-checkbox:after {
  content: '';
  position: absolute;
  left: 7px;
  top: 3px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: rotate(45deg);
}

.save-button {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.save-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}

.save-button:not(:disabled):hover {
  background-color: #2980b9;
}

body {
  background: linear-gradient(135deg, #e0f7fa, #b2ebf2);
  font-family: 'Roboto', sans-serif;
}
</style>

// Install Vue Toastification // Run: npm install vue-toastification --save //
main.js import { createApp } from 'vue'; import App from './App.vue'; import
Toast from "vue-toastification"; import "vue-toastification/dist/index.css";
const app = createApp(App); app.use(Toast, { transition:
"Vue-Toastification__bounce", maxToasts: 5, newestOnTop: true });
app.mount('#app');
