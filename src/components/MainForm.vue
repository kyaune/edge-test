<template>
  <div class="form">
    <div>
      <div class="form__body">
        <div class="form__item">
          <div class="item__label necessarily">Имя</div>
          <FormInput v-model="firstName"/>
        </div>

        <div class="form__item">
          <div class="item__label">Фамилия</div>
          <FormInput v-model="lastName"/>
        </div>

        <div class="form__item">
          <div class="item__label necessarily">Телефон</div>
          <FormInput v-model="telephone"/>
        </div>

        <div class="form__item">
          <div class="item__label necessarily">Почта</div>
          <FormInput v-model="email"/>
        </div>

        <div class="form__item">
          <div class="item__label">Сообщение</div>
          <FormTextArea placeholder="Добавьте свое сообщение" v-model="message"/>
        </div>

        <div class="error" v-if="currentError">
          {{currentError}}
        </div>
        <div class="form__note" v-else>
          * - Обязательные для заполнения поля
        </div>
      </div>

      <div class="form__footer">
        <FlatBtn @click="resetInputs">
          Очистить
        </FlatBtn>
        <div>
          <FlatBtn @click="$emit('close')">
            Закрыть
          </FlatBtn>
          <FlatBtn @click="saveChanges" colored>
            Подтвердить
          </FlatBtn>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
/* eslint-disable */

import { ref } from "vue";
import FormInput from "@/components/inputs/FormInput";
import FlatBtn from '@/components/buttons/FlatBtn'
import FormTextArea from "@/components/inputs/FormTextArea";
const emit = defineEmits(['close'])

const value = ref('')
const currentError = ref()
const firstName = ref('')
const lastName = ref('')
const telephone = ref('')
const email = ref('')
const message = ref('')

const resetInputs = () => {
  firstName.value = ''
  lastName.value = ''
  telephone.value = ''
  email.value = ''
  message.value = ''
  currentError.value = ''
}

const validateName = () => {
  if (firstName.value.trim().length === 0) {
    currentError.value = 'Имя - обязательное поле'
    return false
  }

  if (lastName.value.length <= 100) return true
  else {
    currentError.value = 'Имя должно содержать меньше 100 символов'
    return false
  }
}

const validateLastName = () => {
  if (lastName.value.length <= 100) return true
  else {
    currentError.value = 'Фамилия должна содержать меньше 100 символов'
    return false
  }
}

const validateTelephone = () => {
  const telPattern = /(^8|7|\+7)((\d{10})|(\s\(\d{3}\)\s\d{3}\s\d{2}\s\d{2}))/
  console.log(telPattern.test(telephone.value))
  if (telephone.value.trim().length === 0) {
    currentError.value = 'Телефон - обязательное поле'
    return false
  }

  if (!telPattern.test(telephone.value)) {
    console.log('here')
    currentError.value = 'Введите российский телефонный номер'
    return false
  }

  return true
}

const validateEmail = () => {
  const emailPattern = /(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))/
  console.log('here')

  if (email.value.trim().length === 0) {
    currentError.value = 'Почта - обязательное поле'
    return false
  }

  if (emailPattern.test(email.value)) return true
  else {
    currentError.value = 'Введите валидную электронную почту'
    return false
  }
}

const saveChanges = () => {
  if (!validateName()) return
  if (!validateLastName()) return
  if (!validateTelephone()) return
  if (!validateEmail()) return
  currentError.value = ''
  emit('close')
}

</script>
<style scoped>
.form {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.4);
}

.form > div {
  background-color: rgba(255, 255, 255);
  width: 40%;
}

.form__body {
  padding: 30px;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: center;
}

.form__item {
  padding-top: 20px;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.form__footer {
  background-color: rgba(255, 255, 255);
  padding: 0 10px 20px 20px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  gap: 10px;
}

.form__footer > div {
  display: flex;
  flex-direction: row;
  gap: 10px;
}

.error {
  color: red;
  padding-top: 20px;
}

.necessarily:after {
  color: red;
  content: '*';
}

.form__note {
  padding-top: 20px;
}
</style>
