<template>
    <v-form v-model="valid">
      <v-container>
        <h1>Register</h1>
        <UserAuthForm buttonText="Register" :submitForm="registerUser" hasName="true" />
      </v-container>
    </v-form>
  </template>
  
  <script>
    import UserAuthForm from '@/components/UserAuthForm'

    export default {
        components: {
            UserAuthForm,
        },
        methods: {
            registerUser(registerationinfo) {
              debugger
              alert('You pressed a button')
            }
        }
    }
  </script>

  <style lang="scss" scoped>
    
  </style>