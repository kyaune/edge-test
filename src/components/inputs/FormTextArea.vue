<template>
  <div class="form-input">
    <textarea v-model="vModel" :placeholder="placeholder" maxlength="500"/>
  </div>
</template>
<script setup>
import { computed } from "vue";
/* eslint-disable */
const props = defineProps({
  modelValue: String,
  placeholder: String
})
const emit = defineEmits(['update:modelValue'])

const vModel = computed({
  get() {
    return props.modelValue
  },
  set(val) {
    emit('update:modelValue', val);
  }
})
</script>
<style scoped>
textarea {
  overflow: hidden;
  resize: none;
  width: 100%;
  height: 100%;
}
</style>
