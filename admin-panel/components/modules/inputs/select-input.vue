<template>
  <div class="select-input-container">
    <label :for="`select-input ${label}`">{{ label }}</label>
    <div class="select-input-wrapper">
      <select
        @change="handleInput"
        name="select-input"
        :id="`select-input ${label}`"
      >
        <option value="">{{ optionMessage }}</option>
        <option v-for="option in options" :key="option" :value="option">
          {{ option }}
        </option>
      </select>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  props: {
    optionMessage: {
      type: String,
      default: 'select your option ... ',
    },
    label: {
      type: String,
      default: 'Select input',
    },
    options: {
      type: Array,
      default: () => ['hello', 'hwwear'],
    },
  },
  methods: {
    handleInput(e: any) {
      this.$emit('input', e.target.value);
    },
  },
});
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.select-input-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  .select-input-wrapper {
    position: relative;
    min-width: 340px;
    &::after {
      content: '';
      position: absolute;
      width: 0;
      height: 0;
      border-left: 5px solid transparent;
      border-right: 5px solid transparent;
      border-top: 8px solid $philippine-gray;
      right: 12px;
      top: calc(50% + 5px);
    }
    &::before {
      content: '';
      position: absolute;
      z-index: 1;
      width: 0;
      height: 0;
      border-left: 5px solid transparent;
      border-right: 5px solid transparent;
      border-bottom: 8px solid $philippine-gray;
      right: 12px;
      top: calc(50% - 10px);
    }
  }
  select {
    background-color: $anti-flash-white;
    border: 2px solid $eton-blue;
    outline: none;
    padding: 15px;
    width: 100%;
    border-radius: 10px;
    font-size: 18px;
    font-weight: 300;
    appearance: none;
    position: relative;
    cursor: pointer;
  }
  label {
    margin-bottom: 10px;
    font-size: 18px;
    font-weight: 300;
  }
}
</style>
