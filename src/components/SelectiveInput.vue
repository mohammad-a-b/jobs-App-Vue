<script setup>
const props = defineProps({
  label: String,
  options: Array,      // label, value      
 
  isRequired: {
    type: Boolean,
    default: true,
  },
});

const modelValue = defineModel({
  value: String,
  required: true,
});
</script>

<template>
  <div>
    <label class="input-label">
      {{ label }}
      <span v-if="isRequired" class="red-star-input">*</span>
    </label>
    <select v-model="modelValue" :required="isRequired">
      <option disabled value="" class="disabled-option">انتخاب کنید...</option>
      <option v-for="option in options" :key="option.value" :value="option.value">
        {{ option.label }}
      </option>
    </select>
  </div>
</template>

<style scoped>
div {
  margin-top: 10px;
}
select {
  margin: 5px 0;
  width: 100%;
  padding: 7.2px 12px;
  border: 1px solid #000000;
  border-radius: 8px;
  font-size: 15px;
  cursor: pointer;
}

select:focus {
  border: 1px #3abed5 solid;
  outline: none;
}

.placeholder-active {
  color: #c7c7cc;
  font-size: 15px;
  font-weight: 200;
}
</style>
