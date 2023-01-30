<template>
  <div class="multi-select-wrapper">
    <p class="multi-select-label">{{ label }}</p>
    <div
      class="multi-select"
      @click="handleClick"
      @blur="focused = false"
      tabindex="-1"
      ref="parent"
    >
      <p class="multi-select__placeholder" v-show="showPlaceholder">
        {{ placeholder }}
      </p>
      <div
        class="multi-select__selected"
        v-for="(option, index) in formattedOptions"
        :key="index"
        v-show="option.checked"
      >
        {{ option[displayProperty] }}
        <span
          class="multi-select__remove"
          @click="
            preventClose($event);
            handleOptionClick(index);
          "
        >
          &times;
        </span>
      </div>
      <div
        class="multi-select__options"
        v-show="focused"
        :style="{ top: optionsTop }"
        @click="preventClose"
      >
        <div
          class="multi-select__option"
          :class="{ 'multi-select__option--checked': option.checked }"
          v-for="(option, index) in formattedOptions"
          :key="index"
          @click="handleOptionClick(index)"
        >
          <div class="multi-select__checkbox"></div>
          <div class="multi-select__text">
            {{ option[displayProperty] }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
export default Vue.extend({
  data() {
    return {
      focused: false,
      optionsTop: '324px;',
      showPlaceholder: true,
    };
  },
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    value: {
      type: Array,
      default: () => [],
    },
    placeholder: {
      type: String,
      default: 'click to select',
    },
    label: {
      type: String,
      default: 'Multi select',
    },
    displayProperty: {
      type: String,
      default: 'name',
    },
    valueProperty: {
      type: String,
      default: 'value',
    },
  },
  computed: {
    formattedOptions() {
      let fo = this.options.map((option) => {
        let checked = this.value.some((v) => v === option[this.valueProperty]);

        return { ...option, checked };
      });

      return fo;
    },
  },
  mounted() {
    this.fixTop();
  },
  methods: {
    fixTop() {
      this.optionsTop = this.$refs.parent.clientHeight + 2 + 'px';
    },
    handleClick() {
      this.focused = !this.focused;
    },
    preventClose(e) {
      e.stopPropagation();
    },
    handleOptionClick(index) {
      let clickedValue = this.options[index][this.valueProperty];
      let newValue = [...this.value];

      let existIndex = this.value.findIndex((v) => v === clickedValue);
      console.log(
        '🚀 ~ file: multi-select-input.vue:112 ~ handleOptionClick ~ existIndex',
        existIndex
      );

      if (existIndex === -1) {
        this.showPlaceholder = false;
        newValue.push(clickedValue);
      } else {
        newValue.splice(existIndex, 1);
        if (newValue.length === 0) {
          this.showPlaceholder = true;
        }
      }
      this.$emit('input', newValue);
      setTimeout(this.fixTop, 100);
    },
  },
});
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.multi-select {
  background-color: $anti-flash-white;
  padding: 3px 12px;
  border: 2px solid $eton-blue;
  border-radius: 10px;
  min-height: 44px;
  min-width: 250px;
  max-width: 260px;
  display: flex;
  position: relative;
  align-items: center;
  flex-wrap: wrap;
  &:focus {
    outline: none;
  }
  &::after {
    content: '';
    position: absolute;
    width: 0;
    height: 0;
    border-left: 5px solid transparent;
    border-right: 5px solid transparent;
    border-top: 8px solid $philippine-gray;
    right: 12px;
    top: calc(50% + 3px);
  }
  &::before {
    content: '';
    position: absolute;
    width: 0;
    height: 0;
    border-left: 5px solid transparent;
    border-right: 5px solid transparent;
    border-bottom: 8px solid $philippine-gray;
    right: 12px;
    top: calc(50% - 10px);
  }
}
.multi-select-label {
  font-weight: 300;
  font-size: 16px;
  margin-bottom: 10px;
}
.multi-select__placeholder {
  color: $philippine-gray;
  font-weight: 300;
  font-size: 16px;
}
.multi-select__selected {
  padding: 3px 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 20px;
  margin: 3px 3px;
  background-color: $arsenic;
  color: $white;
}
.multi-select__remove {
  cursor: pointer;
  margin-left: 10px;
  border-radius: 50%;
  background-color: $white;
  color: $arsenic;
  width: 11px;
  height: 11px;
  display: flex;
  align-items: center;
  justify-content: center;
  &:hover {
    color: red;
  }
}
.multi-select__options {
  position: absolute;
  top: 34px;
  right: 0;
  left: 0;
  display: flex;
  background-color: $anti-flash-white;
  flex-direction: column;
  box-shadow: 0 3px 3px 2px $philippine-gray;
  padding: 5px 0;
  min-height: 55px;
  max-height: 188px;
  overflow-y: auto;
}
.multi-select__option {
  padding: 6px 11px;
  cursor: pointer;
  display: flex;
  align-items: center;
  font-weight: 300;
}
.multi-select__option--checked {
  color: #1f7bb8;
  font-weight: bold;
}
.multi-select__checkbox {
  width: 22px;
  height: 22px;
  border: 1px solid #969696;
  margin-right: 7px;
  position: relative;
}
.multi-select__option--checked .multi-select__checkbox {
  border: 1px solid #1f7bb8;
  background-color: #1f7bb8;
}
.multi-select__option--checked .multi-select__checkbox::after {
  width: 11px;
  height: 6px;
  border-left: 2px solid rgb(225, 225, 225);
  border-bottom: 2px solid rgb(225, 225, 225);
  content: '';
  z-index: 10;
  position: absolute;
  transform: rotate(-45deg);
  left: 3px;
  top: 4px;
}
</style>
