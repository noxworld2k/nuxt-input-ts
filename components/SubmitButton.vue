<script setup lang="ts">
interface Props {
  isDisabled: boolean;
}
defineProps<Props>();

</script>

<template>
  <div>
    <button
      class="btn"
      type="submit"
      id="submit"
      :disabled="isDisabled"
      :class="isDisabled ? 'disabled' : 'btn-active'"
    >
      Submit
    </button>
  </div>
</template>

<style lang="scss" scoped>
.btn {
  margin-top: 1rem;
  width: 100%;
  border-radius: 5px;
  background-color: cornflowerblue;
  color: white;
  border: none;
  padding: 0.5rem;
}
.btn-active {
  &:hover {
    background-color: #1e90ff;
  }
  &:active {
    background-color: #1e43ff;
  }
}
.disabled {
  background-color: #ccc;
  color: #666;
}
</style>
