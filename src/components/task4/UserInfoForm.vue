<template>
  <div class="form-container">
    <div>
      <label class="label">
        Ім'я
        <input type="text" :class="['input', emptyBgColor]" v-model="userNameValue" />
      </label>
    </div>
    <div>
      <label class="label">
        Вік
        <input type="number" :class="['input', { [ageBgColor]: userAgeValue !== '' }]" v-model="userAgeValue" />
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserInfoForm',
  props: {
    userName: {
      type: String,
    },
    userNameModifiers: {
      default: () => ({}),
    },
    userAge: {
      type: Number,
    },
    userAgeModifiers: {
      default: () => ({}),
    },
  },
  data() {
    return {
      ageBgColor: null,
      emptyBgColor: null,
    }
  },
  computed: {
    userNameValue: {
      get() {
        return this.userName
      },
      set(newUserName) {
        if (this.userNameModifiers.checkEmpty) {
          newUserName === '' ? (this.emptyBgColor = 'empty') : (this.emptyBgColor = null)
        }
        this.$emit('update:userName', newUserName)
      },
    },
    userAgeValue: {
      get() {
        return this.userAge
      },
      set(newUserAge) {
        if (this.userAgeModifiers.checkAge) {
          newUserAge < 18 ? (this.ageBgColor = 'child') : (this.ageBgColor = 'adult')
        }
        this.$emit('update:userAge', newUserAge)
      },
    },
  },
}
</script>

<style lang="scss" scoped>
.form-container {
  display: grid;
  gap: 1.25rem 0;
}
.child,
.empty {
  background-color: red;
}
.adult {
  background-color: #68c874;
}
</style>
