<template>
  <div class="w-11/12 shadow-md m-10 p-10 pt-0 bg-white rounded-xl">
    <h1 class="font-semibold text-xl py-5">Add Payment Method</h1>
    <div class="flex flex-col-reverse md:flex-row items-center h-full gap-5">
      <FormCreditCard v-model="cardInfo" />
      <CreditCard :card-info="cardInfo" />
    </div>
  </div>
</template>

<script setup lang="ts">
import CreditCard from "@/components/CreditCard.vue";
import FormCreditCard from "@/components/FormCreditCard.vue";
import { ref } from "vue";

const cardInfo = ref({
  cardNumber: "",
  cardholderName: "",
  expirationMonth: "",
  expirationYear: "",
  cvv: "",
});
</script>
