<template>
  <div>
    <label class="toggle">
      <span class="toggle-label">{{ label }}</span>
      <input
        @click="toggleSwitch"
        class="toggle-checkbox"
        type="checkbox"
        :value="inputValue"
        ref="checkbox"
      />
      <div class="toggle-switch"></div>
    </label>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: 'switch',
    },
    inputValue: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      value: this.inputValue,
    };
  },
  methods: {
    toggleSwitch(e) {
      // this.$emit('input', e.target.checked);j
      this.value = !this.value;
      this.$emit('input', e.target.checked);
    },
  },
  mounted() {
    this.$refs.checkbox.checked = this.value;
  },
};
</script>

<style lang="scss" scoped>
@import '@/assets/scss/helpers/variables';
.toggle {
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
}

.toggle-switch {
  display: inline-block;
  background: #d9d9dd;
  border-radius: 16px;
  width: 56px;
  height: 24px;
  position: relative;
  vertical-align: middle;
  transition: background 0.25s;
}
.toggle-switch:before,
.toggle-switch:after {
  content: '';
}
.toggle-switch:before {
  display: block;
  background: $white;
  border-radius: 50%;
  width: 16px;
  height: 16px;
  position: absolute;
  top: 4px;
  left: 4px;
  transition: left 0.25s;
}
.toggle-checkbox:checked + .toggle-switch {
  background: $azure;
}
.toggle-checkbox:checked + .toggle-switch:before {
  left: 36px;
}

.toggle-checkbox {
  position: absolute;
  visibility: hidden;
}

.toggle-label {
  margin-bottom: 5px;
  position: relative;
}
</style>
