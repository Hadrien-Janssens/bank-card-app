<template>
  <form action="" class="basis-1/2 flex flex-col gap-4">
    <label for="card-number" class="text-gray-600 text-xs">
      Card Number
      <Input
        id="card-number"
        v-model="cardInfo.cardNumber"
        placeholder="ex : 67031900395741021 "
        class="outline-none"
      />
    </label>
    <label for="cardholder-number" class="text-gray-600 text-xs">
      Cardholder Name
      <Input
        id="cardholder-number"
        v-model="cardInfo.cardholderName"
        placeholder="ex : John Doe"
      />
    </label>
    <div class="flex justify-between gap-4">
      <label for="cardholder-number" class="text-gray-600 text-xs">
        Expiration Month
        <Input
          id="expiration-month"
          v-model="cardInfo.expirationMonth"
          placeholder="ex : 07"
        />
      </label>
      <label for="cardholder-number" class="text-gray-600 text-xs">
        Expiration Year
        <Input
          id="cardholder-number"
          v-model="cardInfo.expirationYear"
          placeholder="ex : 27"
        />
      </label>
    </div>

    <label for="cvv" class="text-gray-600 text-xs">
      cvv
      <Input id="cvv" v-model="cardInfo.cvv" placeholder="ex : 468" />
    </label>
    <Button class="bg-blue-500 hover:bg-blue-600 transition">Add Card</Button>
  </form>
</template>
<!-- 67031900395741021 -->

<script setup lang="ts">
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

const cardInfo = defineModel();

function luhnCheck(cardNumber: string): boolean {
  // Supprimer les espaces et vérifier que le numéro est composé uniquement de chiffres
  cardNumber = cardNumber.replace(/\D/g, "");
  if (!/^\d+$/.test(cardNumber)) return false;

  let sum = 0;
  let shouldDouble = false;

  // Parcourir le numéro de la carte de droite à gauche
  for (let i = cardNumber.length - 1; i >= 0; i--) {
    let digit = parseInt(cardNumber[i]);

    if (shouldDouble) {
      digit *= 2;
      // Si le doublé est supérieur à 9, on soustrait 9
      if (digit > 9) digit -= 9;
    }

    sum += digit;
    // Alterner pour doubler une fois sur deux
    shouldDouble = !shouldDouble;
  }

  // La somme doit être un multiple de 10 pour être valide
  return sum % 10 === 0;
}
function cvvCheck(cvv: string): boolean {
  return cvv.length === 3 && /^\d+$/.test(cvv);
}
function monthExpirationCheck(month: string): boolean {
  return parseInt(month) <= 12;
}
function yearExpirationCheck(year: string): boolean {
  const currentYear = new Date().getFullYear();
  if (year.length > 2) {
    return false;
  }
  return parseInt(year) >= currentYear.toString().slice(-2);
}

function dateExpirationCheck(month: string, year: string): boolean {
  if (monthExpirationCheck(month) && yearExpirationCheck(year)) {
    const currentYear = new Date().getFullYear().toString().slice(-2);
    const currentMonth = new Date().getMonth() + 1;

    if (currentYear > year) {
      return false;
    } else if (currentYear === year && currentMonth > month) {
      return false;
    }
    return true;
  }
}
</script>
