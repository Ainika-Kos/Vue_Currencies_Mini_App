<template>
  <div class="show-currency-wrapper">
      <div
        v-for="currency in currencies"
        :key="currency.id"
        className="show-currency"
      >
        {{ currency.name }}
        <Button
          label="X"
          @onClick="currency.isActive = !currency.isActive"
        />
      </div>
    </div>
</template>

<style src="./showCurrency.scss" lang="scss" scoped></style>

<script lang="ts">
import { defineComponent } from 'vue';
import Button from '../button/button.vue';

const Component = defineComponent({
  components: {
    Button,
  },
  props: ['currencies'],
});

export default Component;
</script>
