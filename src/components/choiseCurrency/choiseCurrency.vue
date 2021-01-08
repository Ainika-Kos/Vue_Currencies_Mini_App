<template>
  <div class="choise-currency-wrapper">
    <div
      v-for="currency in currencies"
      :key="currency.id"
      class="choise-currency"
      :class="{ activeChoise: currency.isActive }"
      @click="currency.isActive = !currency.isActive"
    >
      <span>
        <span
          class="choise-currency__checkbox"
          :class="{ red: currency.isActive }"
        >
          X
        </span>
      </span>
      <span class="choise-currency__name">{{ currency.name }}</span>
    </div>
  </div>
</template>

<style src="./choiseCurrency.scss" lang="scss" scoped></style>

<script lang="ts">
import { defineComponent } from 'vue';

const Component = defineComponent({
  props: ['currencies'],
});

export default Component;
</script>
