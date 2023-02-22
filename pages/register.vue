<template>
  <v-container>
    <h1>Register</h1>
    <UserAuthForm buttonText="Register" :submitForm="registerUser" hasName="true" />
  </v-container>
</template>
  
<script>
  import UserAuthForm from '@/components/UserAuthForm'

  export default {
    components: {
      UserAuthForm,
    },
    methods: {
      registerUser(registerationinfo) {
        this.$auth.loginWith('local', {
          data: registerationinfo
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  
</style>