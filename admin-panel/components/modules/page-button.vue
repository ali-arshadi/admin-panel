<template>
  <NuxtLink :class="['page-link', active ? 'page-link-active' : '']" :to="url">
    <div class="svg-container" v-html="icon"></div>
    <p class="page-name">{{ name }}</p>
  </NuxtLink>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    name: {
      type: String,
      default: '',
    },
    url: {
      type: String,
      default: '/',
    },
    active: {
      type: Boolean,
      default: true,
    },
    icon: {
      type: String,
      default: `
        <svg width="24" height="24" viewBox="0 0 24 24"  xmlns="http://www.w3.org/2000/svg">
            <path d="M17.82 8.69999C18.53 8.30999 19.4 8.81999 19.39 9.62999L19.35 15.05C19.34 15.87 18.45 16.37 17.75 15.95L13.07 13.15C12.37 12.73 12.39 11.71 13.1 11.32L17.82 8.69999ZM19.25 6.27999C19.4 6.65999 19.17 7.04999 18.81 7.24999L13.18 10.36C12.38 10.8 11.44 10.09 11.64 9.20999L12.86 3.67999C13.01 2.97999 13.8 2.63999 14.42 2.98999L18.34 5.22999C18.77 5.47999 19.08 5.84999 19.25 6.27999Z"/>
            <path d="M12.01 2.67202L9.93998 11.972C9.90998 12.112 9.90998 12.262 9.93998 12.412L11.67 21.092C11.79 21.692 11.28 22.262 10.78 21.892L5.48998 18.122C4.92998 17.722 4.59998 17.082 4.59998 16.402V7.09202C4.59998 6.33202 4.99998 5.63202 5.66998 5.25202L10.96 2.24202C11.11 2.15202 11.27 2.09202 11.43 2.04202C11.81 1.91202 12.09 2.29202 12.01 2.67202Z"/>
            <path d="M17.629 16.81C18.279 17.2 18.319 18.13 17.709 18.57L14.239 21.09C13.619 21.54 12.729 21.2 12.579 20.44L11.559 15.24C11.379 14.34 12.349 13.66 13.139 14.13L17.629 16.81Z"/>
        </svg>
    `,
    },
  },
})
</script>

<style lang="scss">
@import '@/assets/scss/helpers/variables';
.page-link {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  min-height: 60px;
  padding: 0 20px;
  .svg-container {
    width: 24px;
    height: 24px;
    svg {
      width: 100%;
      height: 100%;
      fill: $black;
    }
  }
  .page-name {
    margin-left: 20px;
    text-transform: capitalize;
    font-size: 22px;
  }
  &:hover {
    .svg-container {
      svg {
        fill: $eton-blue;
      }
    }
  }
}
.page-link-active {
  position: relative;
  .svg-container {
    svg {
      fill: $eton-blue;
    }
  }
  &::before {
    content: '';
    position: absolute;
    width: 5px;
    background-color: $eton-blue;
    height: 100%;
    left: 0;
  }
}
</style>
