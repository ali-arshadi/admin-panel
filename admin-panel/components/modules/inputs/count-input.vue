<template>
  <div class="count-input">
    <button class="minus-button" @click="minusCount">
      <IconMinus />
    </button>
    <p>{{ count }}</p>
    <button class="plus-button" @click="plusCount">
      <IconPlus />
    </button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
export default Vue.extend({
  components: {
    IconPlus: () => import('@/components/icons/icon-plus.vue'),
    IconMinus: () => import('@/components/icons/icon-minus.vue'),
  },
  props: {
    max: {
      type: Number,
    },
    min: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      count: this.min,
    };
  },
  methods: {
    minusCount() {
      if (this.count !== this.min) {
        this.count -= 1;
        console.log(
          '🚀 ~ file: count-input.vue:38 ~ minusCount ~ this.count',
          this.count
        );
      } else {
        return;
      }
    },
    plusCount() {
      if (this.count !== this.max) {
        this.count += 1;
        console.log(
          '🚀 ~ file: count-input.vue:49 ~ plusCount ~ this.count',
          this.count
        );
      } else {
        return;
      }
    },
  },
});
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.count-input {
  border: 2px solid $eton-blue;
  background-color: $anti-flash-white;
  padding: 15px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.minus-button {
  display: flex;
  align-items: center;
  margin-right: 20px;
  cursor: pointer;
  background-color: transparent;
  border: none;
}
.plus-button {
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  background-color: transparent;

  margin-left: 20px;
}
</style>
