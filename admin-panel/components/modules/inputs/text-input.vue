<template>
  <div class="text-input-container">
    <label :for="`text-input ${label}`">
      {{ label }}
    </label>
    <input
      type="text"
      :id="`text-input ${label}`"
      :placeholder="placeholder"
      @input="handleInput"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  props: {
    label: {
      type: String,
      default: 'Text input',
    },
    placeholder: {
      type: String,
      default: 'Text input',
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
.text-input-container {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  flex-direction: column;
  label {
    font-size: 18px;
    font-weight: 300;
    margin-bottom: 10px;
  }
  input {
    border: 2px solid $eton-blue;
    padding: 15px;
    border-radius: 10px;
    font-size: 18px;
    font-weight: 300;
    outline: none;
    background-color: $anti-flash-white;
    &::placeholder {
      color: $philippine-gray;
    }
  }
}
</style>
