<template>
  <div class="basis-1/2 flex justify-center">
    <div
      class="w-40 bg-gradient-to-r to-indigo-600 from-blue-500 text-white rounded-lg px-10 py-5 min-w-72 shadow-sm hover:shadow-xl hover:scale-[1.02] duration-300"
    >
      <p class="mt-5 text-md">
        <span class="text-sm">N° </span> {{ cardInfo.cardNumber }}
      </p>
      <p class="mb-5 text-xs">
        <span class="font-extralight">CVV </span> {{ cardInfo.cvv }}
      </p>
      <div class="flex justify-between">
        <div>
          <p class="text-xs font-extralight">CARDHOLDER</p>
          <p class="text-xs">{{ cardInfo.cardholderName }}</p>
        </div>
        <div>
          <p class="text-xs font-extralight">EXPIRES</p>
          <p class="text-xs text-center">
            <span>
              {{ cardInfo.expirationMonth }} /
              {{ cardInfo.expirationYear }}</span
            >
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  cardInfo: Object,
});
</script>
