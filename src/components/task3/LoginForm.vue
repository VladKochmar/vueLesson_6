<template>
  <label class="label">
    Введіть логін
    <input type="text" :class="['input', { 'incorrect-login': isIncorrect }]" v-model="loginValue" />
  </label>
</template>

<script>
export default {
  name: 'LoginForm',
  props: {
    modelValue: {
      type: String,
    },
    modelModifiers: {
      default: () => ({}),
    },
    emails: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      isIncorrect: null,
    }
  },
  computed: {
    loginValue: {
      get() {
        return this.modelValue
      },
      set(newLogin) {
        if (this.modelModifiers.check) {
          if (this.emails.find((email) => email.login === newLogin)) {
            newLogin += '@inv.mn.edu'
            this.isIncorrect = false
          } else {
            this.isIncorrect = true
          }
        }
        this.$emit('update:modelValue', newLogin)
      },
    },
  },
}
</script>

<style lang="scss" scoped>
.incorrect-login {
  background-color: red;
}
</style>
