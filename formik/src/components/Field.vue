<template>
  <div>
    <div v-if="isSelect">
      <select
        :name="name"
        @input="$emit('update:modelValue', $event.target.value)"
      >
        <slot />
      </select>
    </div>
    <div v-else>
      <input
        :name="name"
        :type="as"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';

const isSelect = computed(() => props.as === 'select');

const props = defineProps({
  as: {
    type: String,
    default: 'text',
  },
  name: {
    type: String,
    default: '',
  },
  modelValue: {
    type: String,
    default: '',
  },
});
</script>
