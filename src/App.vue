<script setup>
import { reactive } from "vue";
import BaseInput from "@/components/BaseInput.vue";
import Address from "./components/Address.vue";

const form = reactive({
  name: "Bo Bo",
  email: "",
  age: "345345rr",
  address: {
    no: "",
    street: "",
    quater: "",
  },
});
</script>

<template>
  <div class="flex h-screen justify-center items-center bg-salt-300">
    <div class="grid col-span-12">
      <div class="col-span-12 grid grid-cols-3 gap-8 mb-6">
        <div class="col-span-1">
          <BaseInput v-model="form.name" type="text" name="name" placeholder="Name" />
        </div>
        <div class="col-span-1">
          <BaseInput v-model="form.email" type="text" name="email" placeholder="Email" />
        </div>
        <div class="col-span-1">
          <BaseInput v-model="form.age" type="number" name="age" placeholder="Age" />
        </div>
      </div>
      <Address
        class="col-span-12 grid grid-cols-3 gap-8"
        :placeholder="{ no: 'No', street: 'Street', quarter: 'Quarter' }"
        v-model="form.address"
      />
    </div>
  </div>
</template>
