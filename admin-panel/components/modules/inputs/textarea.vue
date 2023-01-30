<template>
  <div class="textarea-container">
    <label :for="`textarea-input ${label}`">
      {{ label }}
    </label>
    <div class="textarea-input-wrapper">
      <textarea
        name="textarea-input"
        :id="`textarea-input ${label}`"
        :placeholder="placeholder"
        @input="handleInput"
      ></textarea>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  props: {
    label: {
      type: String,
      default: 'Textarea input',
    },
    placeholder: {
      type: String,
      default: 'Textarea input',
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
.textarea-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  textarea {
    width: 340px;
    height: 200px;
    border: 2px solid $eton-blue;
    background-color: $anti-flash-white;
    resize: none;
    border-radius: 10px;
    padding: 15px;
    outline: none;
    font-size: 18px;
    font-weight: 300;
    &::placeholder {
      color: $philippine-gray;
    }
  }
  label {
    font-size: 18px;
    font-weight: 300;
    margin-bottom: 10px;
  }
}
</style>
