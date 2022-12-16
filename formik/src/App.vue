<template>
  <Formik
    :initialValues="{ name: '', email: '', password: '', select: '' }"
    :onSubmit="handleSubmit"
    :validate="validate"
  />
</template>

<script setup>
import { ref } from 'vue';
import Formik from './components/Formik.vue';

const isSubmitting = ref(false);
const switchIsSubmitting = () => {
  isSubmitting.value = !isSubmitting.value;
};
const handleSubmit = (formValues) => {
  switchIsSubmitting();
  const isValid = validate(formValues);

  if (Object.keys(isValid).length === 0) {
    alert('Form is valid');
  } else {
    let errorMessages = '';
    for (const [key, value] of Object.entries(isValid)) {
      errorMessages += `${key}: ${value} \n`;
    }
    alert(errorMessages);
  }
  switchIsSubmitting();
};

const validate = (formValues) => {
  let errors = {};
  if (!formValues.email) {
    errors.email = 'Required';
  } else if (
    !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(formValues.email)
  ) {
    errors.email = 'Invalid email address';
  }

  if (!formValues.password) {
    errors.password = 'Required';
  } else if (formValues.password.length < 8) {
    errors.password = 'Password must be at least 8 characters';
  }

  if (!formValues.name) {
    errors.name = 'Required';
  } else if (formValues.name.length < 3) {
    errors.name = 'Name must be at least 3 characters';
  }

  return errors;
};
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
