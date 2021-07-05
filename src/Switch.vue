<template>
  <label class="switch" :class="classObject">
    <input
      ref="input"
      :disabled="disabled"
      :name="name"
      :value="value"
      @change="handleChange"
      type="checkbox"
    >
  </label>
</template>

<script>
export default {
  props: {
    disabled: Boolean,
    isFullwidth: Boolean,
    type: String,
    size: String,
    name: String,
    value: Boolean
  },

  computed: {
    classObject () {
      const { type, size, value } = this
      return {
        [`is-${type}`]: type,
        [`is-${size}`]: size,
        checked: value
      }
    }
  },

  watch: {
    value () {
      this.applyValue()
    }
  },

  methods: {
    handleChange (event) {
      this.$emit('input', event.target.checked)
    },

    applyValue () {
      this.$refs.input.checked = !!this.value
    }
  },

  mounted () {
    this.applyValue()
  }
}
</script>
