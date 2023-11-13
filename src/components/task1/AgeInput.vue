<template>
  <label class="label">
    Введіть вік
    <input type="number" :class="['input', { [ageBgColor]: userAge !== '' }]" v-model="userAge" />
  </label>
</template>

<script>
export default {
  name: 'AgeInput',
  props: {
    modelValue: {
      type: Number,
    },
    modelModifiers: {
      default: () => ({}),
    },
  },
  data() {
    return {
      ageBgColor: null,
    }
  },
  computed: {
    userAge: {
      get() {
        return this.modelValue
      },
      set(newAge) {
        if (this.modelModifiers.check) {
          if (newAge < 0 || newAge > 150) newAge = null
        }
        if (this.modelModifiers.setColor) this.setBgColor(newAge)
        this.$emit('update:modelValue', newAge)
      },
    },
  },
  methods: {
    setBgColor(currentValue) {
      if (currentValue < 10) this.ageBgColor = 'child'
      else if (currentValue < 21) this.ageBgColor = 'teenager'
      else this.ageBgColor = 'adult'
    },
  },
}
</script>

<style lang="scss" scoped>
.child {
  background-color: #68c874;
}
.teenager {
  background-color: yellow;
}
.adult {
  background-color: orange;
}
</style>
