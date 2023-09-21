<script setup>
import { onMounted, reactive } from "vue";
import BaseInput from "@/components/BaseInput.vue";

// props
const { modelValue } = defineProps({
  modelValue: {
    default: {},
    type: [Object],
    required: false,
  },
  placeholder: {
    default: {},
    type: [Object],
    required: false,
  },
});

// emits
const emits = defineEmits(["update:modelValue"]);

const form = reactive({
  no: "",
  street: "",
  quarter: "",
});

onMounted(() => {
  Object.assign(form, modelValue);
});

// methods
const handlerInput = () => {
  emits("update:modelValue", form);
};
</script>

<template>
  <div class="">
    <div class="col-span-1">
      <BaseInput
        v-model="form.no"
        name="no"
        :placeholder="placeholder.no"
        @input="handlerInput"
      />
    </div>
    <div class="col-span-1">
      <BaseInput
        v-model="form.street"
        name="street"
        :placeholder="placeholder.street"
        @input="handlerInput"
      />
    </div>
    <div class="col-span-1">
      <BaseInput
        v-model="form.quarter"
        name="quarter"
        :placeholder="placeholder.quarter"
        @input="handlerInput"
      />
    </div>
  </div>
</template>
