<template>
  <div class="admin-layout-wrapper">
    <sidebar />
    <Nuxt />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  components: {
    sidebar: () => import('@/components/misc/sidebar.vue'),
  },
})
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.admin-layout-wrapper {
  height: 100vh;
  background-color: $white;
  display: flex;
}
</style>
