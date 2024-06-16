<template>
  <div class="flex flex-col">
    <label v-if="label">{{ label }}</label>
    <input
      :placeholder="placeholder"
      class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      :value="modelValue"
      @input="onInput"
    />
  </div>
</template>

<script>
export default {
  name: "TextInput",
  props: {
    placeholder: String,
    modelValue: String,
    label: String,
  },
  methods: {
    onInput(e) {
      this.$emit("update:modelValue", e.target.value);
    },
  },
};
</script>
