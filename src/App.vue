<template>
  <div class="currenciesApp">
    <ShowCurrency :currencies="filteredCurrenciesList" />
    <ChoiseCurrency :currencies="currencies" />
  </div>
</template>

<style src="./app.scss" lang="scss" scoped></style>

<script lang="ts">
import { defineComponent } from 'vue';
import ShowCurrency from './components/schowCurrency/showCurrency.vue';
import ChoiseCurrency from './components/choiseCurrency/choiseCurrency.vue';

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
    ShowCurrency,
    ChoiseCurrency,
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
