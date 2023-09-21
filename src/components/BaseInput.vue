<script setup>
import { computed, onMounted, ref } from "vue";

// props
const { modelValue, type, name, placeholder } = defineProps({
  modelValue: {
    default: null,
    type: [String, Number, Boolean],
    required: false,
  },
  type: {
    default: "text",
    type: [String],
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
const emits = defineEmits(["update:modelValue"]);

// data
const inputRef = ref(null);

onMounted(() => {
  inputRef.value.value = checkValidation(modelValue);
});

// computed
const getType = computed(() => {
  if (normalize(["text", "number"]).includes(type)) {
    return "text";
  }

  return type;
});

// methods
const normalize = (data) => {
  if (Array.isArray(data)) {
    return data.map((datum) => {
      return datum.toLowerCase();
    });
  } else if (typeof data == "string") {
    return data.toLowerCase();
  }

  return data;
};

const checkValidation = (data) => {
  if (normalize("text") == type) {

    return data;
  } else if (normalize("number") == type) {

    return data.replace(/[^0-9]/g, '');
  }

  return data;
};

const handlerInput = (e) => {
  e.target.value = checkValidation(e.target.value);

  emits("update:modelValue", e.target.value);
};
</script>

<template>
  <div>
    <input
      ref="inputRef"
      class="border p-2 border-gray-400 rounded-md shadow outline-none focus:border-blue-400 focus:border-2"
      :name="name"
      :type="getType"
      :placeholder="placeholder"
      :value="modelValue"
      @input="handlerInput"
    />
  </div>
</template>
