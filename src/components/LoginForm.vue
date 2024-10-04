<template>
  <form @submit.prevent="onSubmit" class="loginform">
    <BaseInput label="Email" type="email" v-model="email" :error="errorMessage" />

    <BaseInput label="Password" type="password" />

    <BaseButton type="submit" class="-fill-gradient"> Submit </BaseButton>
  </form>
</template>

<script>
import BaseInput from './BaseInput.vue'
import BaseButton from './BaseButton.vue'
import { useField } from 'vee-validate'
export default {
  setup() {
    function onSubmit() {
      alert('Submitted')
    }
    const { value, errorMessage } = useField('email', function (value) {
      if (!value) return 'This field is required'
      const regex =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      if (!regex.test(String(value).toLowerCase())) {
        return 'Please enter a valid email address'
      }
      return true
    })

    return {
      onSubmit,
      email: value,
      errorMessage: errorMessage
    }
  },
  components: {
    BaseInput,
    BaseButton
  }
}
</script>
