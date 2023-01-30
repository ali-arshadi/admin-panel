<template>
  <div class="logout-component-wrapper">
    <IconLogout />
    <p>Logout</p>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  components: {
    IconLogout: () => import('@/components/icons/icon-logout.vue'),
  },
})
</script>

<style lang="scss">
@import '@/assets/scss/helpers/variables';
.logout-component-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  p {
    margin-left: 5px;
    color: $arsenic;
    font-size: 18px;
  }
  &:hover {
    svg {
      path {
        stroke: $red;
      }
    }
    p {
      color: $red;
    }
  }
}
</style>
