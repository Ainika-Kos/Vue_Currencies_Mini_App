<template>
  <input
    class="inputTask"
    type="text"
    placeholder="Enter your task"
    :value="value"
    @input="updateValue($event.target.value)"
  />
</template>

<style src="./input.scss" lang="scss" scoped></style>

<script lang="ts">
import { defineComponent } from 'vue';

const Component = defineComponent({
  props: {
    value: String,
  },

  methods: {
    updateValue(value: string) {
      this.$emit('input', value);
    },
  },
});

export default Component;
</script>
