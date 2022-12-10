<template>
  <div class="localization-container">
    <p>{{ label }}</p>
    <div class="localization-input-wrapper">
      <select @change="getSelectedLang" name="localization" id="localization">
        <option v-for="language in languages" :key="language" :value="language">
          {{ language }}
        </option>
      </select>
    </div>
  </div>
</template>

<script lang="ts">
//* We have 3 things to work with
//* Label prop that sets the label of the localization input
//* Languages prop that sets the language of the localization input
//* selectedLang emit that sets the languages of the localization input
import Vue from 'vue'
export default Vue.extend({
  props: {
    label: {
      type: String,
      default: 'Localization',
    },
    languages: {
      type: Array,
      default: ['en(English)'],
    },
  },
  methods: {
    getSelectedLang(e: any) {
      this.$emit('selectedLang', e.target.value)
    },
  },
})
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.localization-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  .localization-input-wrapper {
    position: relative;
    width: 190px;
    &::after {
      content: '';
      position: absolute;
      width: 0;
      height: 0;
      border-left: 8px solid transparent;
      border-right: 8px solid transparent;
      border-top: 8px solid $philippine-gray;
      right: 12px;
      top: calc(50% - 3px);
    }
  }
  select {
    background-color: $anti-flash-white;
    border: 2px solid $eton-blue;
    border-radius: 10px;
    padding: 6px 12px;
    appearance: none;
    width: 100%;
    font-size: 16px;
    font-weight: 300;
  }
  p {
    font-size: 16px;
    font-weight: 300;
    margin-bottom: 10px;
  }
}
</style>
