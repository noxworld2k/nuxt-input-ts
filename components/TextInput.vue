<script setup lang="ts">
import { ref } from "vue";

interface Props {
  label: string;
  placeholder: string;
  disabled: boolean;
  icon: string;
}

defineProps<Props>();


const emit = defineEmits(["update:valid", "update:value"]);

const text = ref("");
const error = ref("");
const textIsValid = ref(false);

const validateInput = (min: number, max: number) => {
  if (text.value.length < min) {
    error.value = "Type at least 3 characters";
    textIsValid.value = false;
  } else if (text.value.length > max) {
    error.value = "Type less than 16 characters";
    textIsValid.value = false;
  } else {
    error.value = "";
    textIsValid.value = true;
  }
  emit("update:valid", textIsValid.value);
  emit("update:value", text.value);
};
</script>

<template>
  <div class="input-box">
    <label for="text-input">{{ label }}</label>
    <input
      id="textInput"
      type="text"
      name="text"
      class="text-input"
      :placeholder="$props.placeholder"
      v-model="text"
      @focusout="validateInput(3,16)"
      :class="[
        error ? 'input-error' : '',
        $props.disabled ? 'input-disabled' : '',
        $props.icon,
      ]"
    />
    <p v-if="error" class="error-text">
      {{ error }}
    </p>
  </div>
</template>

<style scoped lang="scss">
.input-box {
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  margin: 1rem 0;
  width: 300px;
}
.text-input {
  box-sizing: border-box;
  width: 100%;
  height: 2rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  color: #ccc;
  padding: 0.5rem;
  margin-top: 0.5rem;
  &:focus {
    box-shadow: 0 5px 20px -5px rgba(66, 68, 90, 0.49);
    outline: none;
  }
  &:hover,
  &:focus {
    color: #0a0a0a;
  }
}
.input-error {
  border: 1px solid red;
  color: #0a0a0a;
}
.error-text {
  color: red;
}

.icon__left {
  background: url("@/assets/icon_car.png") no-repeat scroll 5px 5px;
  background-position-x: 2%;
  background-position-y: center;
  background-size: 15px;
  padding-left: 2rem;
}
.icon__right {
  background: url("@/assets/icon_car.png") no-repeat ;
  background-position-x: 98%;
  background-position-y: center;
  background-size: 15px;
}
</style>
