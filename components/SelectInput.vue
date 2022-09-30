<script setup lang="ts">
import { ref } from "vue";

interface SelectInputProps {
  label: string;
  options: string[];
  disabled?: boolean;
}
const props = defineProps<SelectInputProps>();

const emits = defineEmits(["update:valid", "update:value"]);
const emitOnSelect = () => {
  validate();
  emits("update:valid", isValid);
  emits("update:value", selectedOption);
};

const selectedOption = ref("");
const isValid = ref(false);
const error = ref("");

const validate = () => {
  if (selectedOption.value === "") {
    error.value = "Please select a brand";
    isValid.value = false;
  } else {
    error.value = "";
    isValid.value = true;
  }
};
</script>
<template>
  <div class="input">
    <label for="select-input">{{ label }}</label>
    <select
      id="select-input"
      name="selectedOption"
      v-model="selectedOption"
      @change="emitOnSelect"
      class="select-input"
      :disabled="props.disabled"
    >
      <option class="select-input-option" selected disabled>Select</option>
      <option
        class="select-input-option"
        v-for="option in options"
        :key="option.id"
        :value="option"
      >
        {{ option }}
      </option>
    </select>
    <p v-if="error">
      {{ error }}
    </p>
  </div>
</template>
<style lang="scss" scoped>
.select-input {
  width: 100%;
  height: 2rem;
  border: 1px solid #ccc;
  color: #ccc;
  border-radius: 4px;
  padding: 0.5rem;
  margin-top: 0.5rem;
  background: url("@/assets/icon_arrow_down.png") no-repeat scroll 5px 5px;
  background-size: 20px;
  background-position-x: 95%;
  appearance: none;
  &:active,
  &:focus {
    background: url("@/assets/icon_arrow_up.png") no-repeat scroll 5px 5px;
    background-size: 20px;
    background-position-x: 95%;
    color: #000;
  }
  &:hover {
    color: #000;
  }
}
</style>
