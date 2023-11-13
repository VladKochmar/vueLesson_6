<template>
  <label class="label">
    Введіть шлях до файлу js
    <input type="text" :class="['input', { 'incorrect-path': isPathIncorrect }]" v-model="pathValue" />
  </label>
</template>

<script>
export default {
  name: 'PathInput',
  props: {
    modelValue: {
      type: String,
    },
    modelModifiers: {
      default: () => ({}),
    },
  },
  data() {
    return {
      isPathIncorrect: null,
    }
  },
  computed: {
    pathValue: {
      get() {
        return this.modelValue
      },
      set(newPath) {
        if (this.modelModifiers.checkPath) {
          this.checkPath(newPath)
        }
        this.$emit('update:modelValue', newPath)
      },
    },
  },
  methods: {
    checkPath(path) {
      if (path.endsWith('.js') || path === null) this.isPathIncorrect = false
      else this.isPathIncorrect = true
    },
  },
}
</script>

<style lang="scss" scoped>
.incorrect-path {
  background-color: red;
}
</style>
