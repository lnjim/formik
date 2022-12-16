<template>
  <div v-for="(value, key) in initialValues">
    <div v-if="isSelect(key)">
      <label :for="key">{{ key }}: </label>
      <Field
        :name="key"
        :as="key"
        @update:modelValue="initialValues[key] = $event"
      >
        <option value="null">Veuillez choisir une option</option>
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
        <option value="option3">Option 3</option>
      </Field>
    </div>
    <div v-else>
      <label :for="key">{{ key }}: </label>
      <Field
        :name="key"
        :as="key"
        @update:modelValue="initialValues[key] = $event"
      />
    </div>
  </div>
  <input type="submit" @click="onSubmit(initialValues)" />
</template>

<script setup>
import { defineProps } from 'vue';
import Field from './Field.vue';

const isSelect = (key) => key === 'select';

const props = defineProps({
  initialValues: {
    type: Object,
    default: () => ({}),
  },
  onSubmit: {
    type: Function,
    default: () => {},
  },
  validate: {
    type: Function,
    default: () => {},
  },
});
</script>
