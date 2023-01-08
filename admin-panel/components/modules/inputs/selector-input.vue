<template>
  <div class="selector-input-component">
    <form class="selector-form">
      <div
        v-for="(option, index) in options"
        :key="option[propertyName]"
        :class="[
          'selector-input-wrapper',
          option[propertyName],
          `option-number-${index}`,
          activeItem === index ? 'active' : '',
        ]"
        :target-data="`option-number-${index}`"
      >
        <input
          type="radio"
          name="selector-input"
          :value="option[propertyValue]"
        />
        <p
          @click="getCoordinate($event, index)"
          for="plan1"
          ref="options"
          :class="['input-name']"
        >
          {{ option[propertyName] }}
        </p>
      </div>
      <div class="animation-rectangle" ref="rectangle"></div>
    </form>
  </div>
</template>

<script>
import Vue from 'vue';
export default Vue.extend({
  data() {
    return {
      activeItem: null,
    };
  },
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    propertyValue: {
      type: String,
      default: 'value',
    },
    propertyName: {
      type: String,
      default: 'name',
    },
    selectedOption: {
      type: Object,
      default: () => {},
    },
  },
  mounted() {
    //* defining rectangle width at first
    if (this.selectedOption) {
      const setSelectedOptionItemWidth = (refs) => {
        let rectangle = refs.rectangle;
        const propertyName = this.propertyName;
        const selectedOption = this.selectedOption;
        const index = this.options.findIndex((element) => {
          return element[propertyName] === selectedOption[propertyName];
        });
        const secondOption = refs.options[index];
        const width = secondOption.offsetWidth;
        rectangle.style.width = width + 'px';
        rectangle.style.left = secondOption.offsetLeft + 'px';
        this.activeItem = index;
        this.$emit('input', secondOption.previousElementSibling.value);
      };
      setTimeout(() => {
        setSelectedOptionItemWidth(this.$refs);
      }, 100);
    } else {
      const setFirstSelectedItemWidth = (refs) => {
        let rectangle = refs.rectangle;
        const firstOption = refs.options[0];
        const width = firstOption.offsetWidth;
        rectangle.style.width = width + 'px';
        this.activeItem = 0;
        this.$emit('input', firstOption.previousElementSibling.value);
      };
      setTimeout(() => {
        setFirstSelectedItemWidth(this.$refs);
      }, 200);
    }
  },
  methods: {
    getCoordinate(e, index) {
      this.activeItem = index;
      let rectangle = this.$refs.rectangle;
      //* position the rectangle by the position of element
      rectangle.style.left = e.target.offsetLeft + 'px';
      //* defining the rectangle width by text width + padding
      const width = e.target.offsetWidth;
      rectangle.style.width = width + 'px';

      this.selectPlan(e);
    },
    selectPlan(e) {
      this.$emit('input', e.target.previousElementSibling.value);
    },
  },
});
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.selector-input-component {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.selector-form {
  position: relative;
  background: $anti-flash-white;
  border-radius: 10px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 3px 3px;
  min-width: 150px;
  border: 2px solid $eton-blue;
  div {
    &:last-child {
      p {
        margin-right: 0px;
      }
    }
  }

  p {
    z-index: 5;
    cursor: pointer;
    position: relative;
    z-index: 5;
    padding: 0px 20px;
    height: 34px;
    display: flex;
    align-items: center;
    user-select: none;
    justify-content: center;
    color: $philippine-gray;
  }

  input {
    display: none;
  }
}
.active {
  p {
    color: $anti-flash-white;
  }
}
.animation-rectangle {
  position: absolute;
  width: 100px;
  height: 90%;
  background-color: $arsenic;
  border-radius: 8px;
  box-shadow: 11px 7px 5px rgba(22, 68, 45, 0.01),
    6px 4px 4px rgba(22, 68, 45, 0.02), 3px 2px 3px rgba(22, 68, 45, 0.04),
    1px 0px 2px rgba(22, 68, 45, 0.04), 0px 0px 0px rgba(22, 68, 45, 0.04);
  transition: all 0.2s cubic-bezier(0.08, 1, 0.88, 1.16);
  left: 5px;
}
</style>
