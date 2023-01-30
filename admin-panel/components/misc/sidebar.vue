<template>
  <div class="sidebar-wrapper">
    <div class="sidebar-header-wrapper">
      <h1>Admin Panel</h1>
    </div>
    <div class="sidebar-pages-wrapper">
      <PageButton
        :name="page.name"
        :url="page.pageUrl"
        v-for="(page, index) in pages"
        :key="index"
      />
    </div>
    <div class="sidebar-footer-wrapper">
      <div class="notification-wrapper">
        <IconNotifications />
      </div>
      <div class="logout-wrapper">
        <Logout />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  data() {
    return {
      pages: [
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
        {
          name: 'dashboard',
          pageUrl: '/',
        },
      ],
    }
  },
  components: {
    IconNotifications: () =>
      import('@/components/icons/icon-notifications.vue'),
    Logout: () => import('@/components/misc/logout.vue'),
    PageButton: () => import('@/components/modules/page-button.vue'),
  },
})
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.sidebar-wrapper {
  min-height: 100vh;
  background-color: $bright-gray;
  width: 320px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 50px 0px;
}
.sidebar-pages-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: space-between;
  justify-content: flex-start;
  overflow-y: auto;
  gap: 20px;
  grid-gap: 20px;
  height: 50%;
  margin-bottom: 50px;
  scrollbar-color: $eton-blue transparent;
  scrollbar-width: thin;
  &::-webkit-scrollbar {
    width: 7px;
    background-color: transparent;
  }
  &::-webkit-scrollbar-thumb {
    background-color: $eton-blue;
  }
}
.sidebar-footer-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 0 25px;
}
</style>
