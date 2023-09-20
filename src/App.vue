<script setup>
import { reactive } from "vue";
import BaseInput from "@/components/BaseInput.vue";
import Address from "./components/Address.vue";

const form = reactive({
  name: "",
  email: "",
  address: {
    no: "",
    street: "",
  },
});
</script>

<template>
  <div class="flex h-screen justify-center items-center bg-salt-300">
    <div class="grid col-span-12">
      <div class="col-span-12 grid grid-cols-2 gap-8 mb-6">
        <div class="col-span-1">
          <BaseInput v-model="form.name" name="name" placeholder="Name" />
        </div>
        <div class="col-span-1">
          <BaseInput v-model="form.email" name="email" placeholder="Email" />
        </div>
      </div>
      <Address
        class="col-span-12 grid grid-cols-2 gap-8"
        :placeholder='{"no": "No", "street": "Street"}'
        v-model="form.address"
      />
    </div>
  </div>
</template>
