<template>
  <div class="currenciesApp">
    <div class="show-currency-wrapper">
      <div
        v-for="currency in filteredCurrenciesList"
        :key="currency.id"
        className="show-currency"
      >
        {{ currency.name }}
        <Button
          label="X"
          class="xButton"
          @onClick="currency.isActive = !currency.isActive"
        />
      </div>
    </div>
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
  </div>
</template>

<style src="./app.scss" lang="scss" scoped></style>

<script lang="ts">
import { defineComponent } from 'vue';
import Button from './components/button/button.vue';

type Currency = {
  id: number;
  name: string;
  isActive: boolean;
};

type Data = {
  currencies: Currency[];
};

const Component = defineComponent({
  components: {
    Button,
  },
  data(): Data {
    return {
      currencies: [
        { id: 1, name: 'eur', isActive: false },
        { id: 2, name: 'pln', isActive: false },
        { id: 3, name: 'gel', isActive: false },
        { id: 4, name: 'dkk', isActive: false },
        { id: 5, name: 'czk', isActive: false },
        { id: 6, name: 'gbp', isActive: false },
        { id: 7, name: 'sek', isActive: false },
        { id: 8, name: 'usd', isActive: false },
        { id: 9, name: 'rub', isActive: false },
      ],
    };
  },
  computed: {
    filteredCurrenciesList(): Currency[] {
      const filtresdCurrencies = this.currencies.filter(
        (item) => item.isActive,
      );

      return filtresdCurrencies;
    },
  },
  methods: {
    changeCurrencyStatus(id: number) {
      const index = this.currencies.findIndex((item) => item.id === id);

      this.currencies[index].isActive = !this.currencies[index].isActive;
    },
  },
});

export default Component;
</script>
