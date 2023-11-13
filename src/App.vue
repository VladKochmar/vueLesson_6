<template>
  <div class="main-block">
    <div class="main-block__container">
      <h1 class="main-title">Урок №6</h1>
      <section class="block">
        <h2 class="title">Завдання №1</h2>
        <div class="block__body">
          <age-input v-model.check.setColor="userAge" />
        </div>
      </section>
      <section class="block">
        <h2 class="title">Завдання №2</h2>
        <div class="block__body">
          <path-input v-model.checkPath="filePath" />
        </div>
      </section>
      <section class="block">
        <h2 class="title">Завдання №3</h2>
        <div class="block__body">
          <login-form v-model.check="userLogin" :emails="loginsList" />
        </div>
      </section>
      <section class="block">
        <h2 class="title">Завдання №4</h2>
        <div class="block__body">
          <user-info-form v-model:userName.checkEmpty="userFormName" v-model:userAge.checkAge="userFormAge" />
        </div>
      </section>
      <section class="block">
        <h2 class="title">Завдання №5</h2>
        <div class="block__body">
          <products-manager :products-list="laptops" />
        </div>
      </section>
      <section class="block">
        <h2 class="title">Завдання №6</h2>
        <div class="block__body">
          <pay-form
            v-model:cardNumber="payCardNumber"
            v-model:expiryDate="payExpiryDate"
            v-model:secureCode="payCardPassword"
          />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import AgeInput from '@/components/task1/AgeInput.vue'
import PathInput from '@/components/task2/PathInput.vue'
import LoginForm from '@/components/task3/LoginForm.vue'
import UserInfoForm from '@/components/task4/UserInfoForm.vue'
import ProductsManager from '@/components/task5/ProductsManager.vue'
import PayForm from '@/components/task6/PayForm.vue'

import { emailsList } from '@/constants/emails'
import { laptopsCatalog } from '@/constants/laptopsCatalog'

export default {
  name: 'App',
  components: { AgeInput, PathInput, UserInfoForm, PayForm, LoginForm, ProductsManager },
  data() {
    return {
      // Task 1
      userAge: null,

      // Task 2
      filePath: null,

      // Task 3
      userLogin: null,
      loginsList: emailsList,

      // Task 4
      userFormName: null,
      userFormAge: null,

      // Task 5
      laptops: laptopsCatalog,

      // Task 6
      payCardNumber: null,
      payExpiryDate: null,
      payCardPassword: null,
    }
  },
}
</script>

<style lang="scss">
@import './assets/styles';
</style>
