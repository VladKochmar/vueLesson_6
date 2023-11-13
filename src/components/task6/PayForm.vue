<template>
  <div class="pay-form">
    <label class="pay-form__label">
      <span>card number</span>
      <input type="text" class="input" v-model="cardNumberValue" @keydown="onKeyDown" />
    </label>
    <div class="pay-form__block">
      <label class="pay-form__label">
        <span>expiry date</span>
        <input type="text" class="input" v-model="expiryDateValue" @keydown="onKeyDown" />
      </label>
      <label class="pay-form__label">
        <span>secure code</span>
        <input type="password" class="input" v-model="secureCodeValue" @keydown="onKeyDown" />
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PayForm',
  props: {
    cardNumber: {
      type: Number,
    },
    expiryDate: {
      type: String,
    },
    secureCode: {
      type: Number,
    },
  },

  data() {
    return {
      cardNumberValue: null,
      expiryDateValue: null,
      secureCodeValue: null,
    }
  },

  watch: {
    cardNumberValue(newNumber, oldNumber) {
      this.cardNumberValue = newNumber.replace(/\D/g, '')
      this.cardNumberValue = newNumber.replace(/(\d{4}(?=\S+))/g, '$1 ')

      if (newNumber.length === 20 && oldNumber.length === 19) this.cardNumberValue = oldNumber
      this.$emit('update:cardNumber', this.cardNumberValue)
    },

    expiryDateValue(newValue, oldValue) {
      if (newValue.length === 2 && oldValue.length === 1) this.expiryDateValue = newValue + '/'
      else if (newValue.length === 2 && oldValue.length === 3) this.expiryDateValue = newValue[0]
      else if (newValue.length === 6 && oldValue.length === 5) this.expiryDateValue = oldValue

      if (newValue[0] > 1) this.expiryDateValue = 0
      if (newValue[0] === '1' && newValue[1] > 2) this.expiryDateValue = 12
      this.$emit('update:expiryDate', this.expiryDateValue)
    },

    secureCodeValue(newCode, oldCode) {
      if (newCode.length === 4 && oldCode.length === 3) this.secureCodeValue = oldCode
      this.$emit('update:secureCode', this.secureCodeValue)
    },
  },

  methods: {
    onKeyDown(event) {
      const key = event.key
      const isDigit = key >= '0' && key <= '9'
      const isBackspace = key === 'Backspace'
      if (!isDigit && !isBackspace) event.preventDefault()
    },
  },
}
</script>

<style lang="scss" scoped>
.pay-form {
  max-width: 31.25rem;
  display: grid;
  gap: 1rem 0;
  // .pay-form__label
  &__label {
    display: grid;
    gap: 0.3125rem 0;
    span {
      text-transform: uppercase;
    }
  }
  // .pay-form__block
  &__block {
    display: flex;
    gap: 0 0.625rem;
  }
}
</style>
