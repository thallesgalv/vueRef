<template>
  <div>
    <label :for="identifier"> {{ label }}: </label>
    <input
      type="text"
      :id="identifier"
      :name="identifier"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      autoComplete="off"
      :maxlength="maxLength"
      required
    />
  </div>
</template>

<script>
export default {
  name: "TextInput",
  props: {
    label: {
      type: String,
      required: true,
    },
    identifier: {
      type: String,
      required: true,
    },
    modelValue: {
      type: String,
    },
    maxLength: {
      type: Number,
    },
  },
  emits: ["update:modelValue"],
};
</script>
