<template>
  <div class="y-input" 
    :class="[
      inputSize ? 'y-input--' + inputSize : '',
    ]">
    <template>
      <input 
        type="text"
        class="y-input__inner"
        v-bind="$props"
        v-model:value="currentValue"
        @blur="handleBlur"
        :disabled="disabled"
        @focus="handleFocus"
        v-bind:class='{"is-error":status=="error"}'
      >
      <span v-if="showClear" class="y-input__suffix">
        <span class="y-input__suffix-inner">
            <i class="iconfont el-input__icon" @click="clear">&#xe644;</i>
        </span>
      </span>
    </template>
    <template>
      <textarea></textarea>
    </template>
  </div>
</template>
<style lang="scss">
</style>
<script>
  import './input.scss';
  import '../../../font/iconfont.css'
  export default {
    name: 'y-input',
    data() {
      return {
        currentValue: this.value,
        prefixOffset: null,
        suffixOffset: null,
        hovering: false,
        focused: false
      };
    },
    props: {
      value: {
        type:  [String, Number],
        default: ''
      },
      status: {
        type:  [String],
        default: 'primary'
      },
      placeholder: String,
      size: String,
      name: String,
      form: String,
      id: String,
      maxlength: Number,
      minlength: Number,
      readonly: Boolean,
      autofocus: Boolean,
      disabled: Boolean,
      type: {
        type: String,
        default: 'text'
      },
      suffixIcon: String,
      prefixIcon: String,
      label: String,
      clearable: {
        type: Boolean,
        default: false
      }
    },
    computed: {
        inputSize() {
          return this.size;
        },
        showClear(){
            return this.clearable && !this.disabled && this.currentValue !== '' && (this.focused || this.hovering);
        }
    },
    mounted() {
     
    },
    methods: {
        handleBlur(event) {
          this.focused = false;
          this.$emit('blur', this.currentValue);
        },
        handleFocus(event) {
            this.focused = true;
            this.$emit('focus', event);
        },
        clear(){
            this.$emit('input', '');
            this.$emit('change', '');
            this.$emit('clear');
            this.currentValue = '';
        }
    }
  };
</script>