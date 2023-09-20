<script setup>

// props
const props = defineProps({
  modelValue: {
    default: null,
    type: [String, Number, Boolean],
    required: false,
  },
  name: {
    default: "name",
    type: [String],
    required: true,
  },
  placeholder: {
    default: "",
    type: [String],
    required: false,
  },
});

// emits
const emits = defineEmits(['update:modelValue']);

// methods
const handlerInput = (e) => {
    emits('update:modelValue', e.target.value);
}

</script>

<template>
  <div>
    <input
      class="border p-2 border-gray-400 rounded-md shadow outline-none focus:border-blue-400 focus:border-2"
      :name="name"
      type="text"
      :placeholder="placeholder"
      :value="modelValue"
      @input="handlerInput"
    />
  </div>
</template>
