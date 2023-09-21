<script setup>
import { computed, ref } from "vue";

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
const currentValue = ref('');

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

const checkValidation = (e) => {
  let typingValue = e.target.value;

  if (normalize("text") == type) {
    return typingValue;
  } else if (normalize("number") == type) {
    const reg = new RegExp("^[0-9]+$");

    if (reg.test(typingValue)) {
      currentValue.value = typingValue;
      return currentValue.value;
    } else {
      e.target.value = currentValue.value;
      return currentValue.value;
    }
  }

  return typingValue;
};

const handlerInput = (e) => {
  emits("update:modelValue", checkValidation(e));
};
</script>

<template>
  <div>
    <input
      class="border p-2 border-gray-400 rounded-md shadow outline-none focus:border-blue-400 focus:border-2"
      :name="name"
      :type="getType"
      :placeholder="placeholder"
      :value="modelValue"
      @input="handlerInput"
    />
  </div>
</template>
