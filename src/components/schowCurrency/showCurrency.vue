<template>
  <div
    v-for="currency in currencies"
    :key="currency.id"
    class="currency-wrapper"
  >
    <div className="currency">
      {{ currency.name }} {{currency.id}}
      <Button label="X" @onClick="currency.isActive = !currency.isActive" />
    </div>
  </div>
</template>

<style src="./showCurrency.scss" lang="scss" scoped></style>

<script lang="ts">
import { defineComponent } from 'vue';

const Component = defineComponent({
  props: ['label', 'currencies'],
});

export default Component;
</script>
