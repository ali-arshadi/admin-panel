<template>
  <div class="search-input-wrapper">
    <IconSearch />
    <input type="text" :placeholder="placeholder" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  props: {
    placeholder: {
      type: String,
      default: 'Search',
    },
  },
  components: {
    IconSearch: () => import('@/components/icons/icon-search.vue'),
  },
  methods: {
    //* this is where the search function should be written
  },
});
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.search-input-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 250px;
  svg {
    position: absolute;
    left: 15px;
  }
  input {
    width: 100%;
    background-color: $anti-flash-white;
    border: 2px solid $eton-blue;
    border-radius: 10px;
    padding: 15px 15px 15px 50px;
    outline: none;
    font-size: 16px;
    font-weight: 300;
  }
}
</style>
