<script setup>
import { computed, onMounted, reactive, ref } from "vue";

// props
const { modelValue, type, name, placeholder, rounded, border, padding } =
  defineProps({
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
    rounded: {
      default: "rounded",
      type: [String],
      required: false,
    },
    border: {
      default: "border",
      type: [String],
      required: false,
    },
    padding: {
      default: "px-2 py-1",
      type: [String],
      required: false,
    },
  });

// emits
const emits = defineEmits(["update:modelValue"]);

// data
const inputRef = ref(null);
const classes = reactive([]);

onMounted(() => {
  initClasses();

  initValue();
});

// computed
const getType = computed(() => {
  if (normalize(["text", "number"]).includes(type)) {
    return "text";
  }

  return type;
});

const getName = computed(() => {
  return name;
});

const getPlaceholder = computed(() => {
  return placeholder;
});

// methods
const initValue = () => {
  inputRef.value.value = checkValidation(modelValue);
};

const setRounded = () => {
  classes.push(rounded);
};

const setBorder = () => {
  classes.push(border);
};

const setPadding = () => {
  classes.push(padding);
};

const getClasses = computed(() => {
  return classes.join(" ");
});

const initClasses = () => {
  setRounded();

  setBorder();

  setPadding();
};

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
    return data.replace(/[^0-9]/g, "");
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
    <!-- class="border p-2 border-gray-400 rounded-md shadow outline-none focus:border-blue-400 focus:border-2" -->

    <input
      ref="inputRef"
      :class="getClasses"
      :name="getName"
      :type="getType"
      :placeholder="getPlaceholder"
      :value="modelValue"
      @input="handlerInput"
    />
  </div>
</template>
