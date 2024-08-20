<template>
  <label>
    <input type="checkbox" @change="onChange" v-model="model" />
    {{ label }}
  </label>
</template>

<script setup>
defineProps({
  label: String,
});
const emits = defineEmits(["check", "uncheck"]);
const model = defineModel();

const onChange = (event) => {
  if (event.currentTarget.checked) {
    emits("check", event.currentTarget);
  } else {
    emits("uncheck", event.currentTarget);
  }
};
</script>
<style></style>
