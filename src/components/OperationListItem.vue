<template>
  <div>
    <input
      class="item-input"
      type="text"
      placeholder="New operation"
      v-model="operation.source"
      v-el:operation-input
      @keyup.enter="onKeyEnter" @keyup.8="onKeyDelete"
      @keydown.up.prevent="onKeyUp" @keydown.down.prevent="onKeyDown"
      @focus="onFocus" @blur="onBlur"></input>
  </div>
</template>

<script>
  export default {
    props: {
      operation: 'Object',
      index: 'Number'
    },

    methods: {
      onKeyEnter (e) {
        this.$dispatch('on-key-enter', this, e)
      },

      onKeyDelete (e) {
        this.$dispatch('on-key-delete', this, e)
      },

      onKeyUp (e) {
        this.$dispatch('on-key-up', this, e)
      },

      onKeyDown (e) {
        this.$dispatch('on-key-down', this, e)
      },

      onFocus (e) {
        this.$dispatch('on-focus', this, e)
      },

      onBlur (e) {
        this.$dispatch('on-blur', this, e)
      },

      focus () {
        this.$els.operationInput.focus()
      }
    }
  }
</script>

<style scoped>
  .item-input {
    padding: 8px;
    box-sizing: border-box;
    width: 100%;
    border-style: none;
    border-bottom: 1px solid #ddd;
    font-family: 'Source Code Pro';
    font-size: 12px;
  }

  .item-input:focus {
    outline: 0;
    border-left: 5px solid #ddd;
  }
</style>
