<template>
  <div class="new-data-wrapper">
    <IconAdd />
    <p>{{ title }}</p>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    title: {
      type: String,
      default: 'Add new data',
    },
  },
  components: {
    IconAdd: () => import('@/components/icons/icon-add.vue'),
  },
})
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.new-data-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 20px 15px;
  background-color: $anti-flash-white;
  p {
    margin-top: 20px;
    color: #578564;
  }
}
</style>
