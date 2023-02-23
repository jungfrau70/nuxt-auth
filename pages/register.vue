<template>
  <v-container>
    <h1>Register</h1>
    <UserAuthForm
      button-text="Register"
      :submit-form="registerUser"
      has-name="true"
    />
  </v-container>
</template>
  
<script>
import UserAuthForm from '@/components/UserAuthForm'

export default {
  components: {
    UserAuthForm,
  },
  methods: {
    async registerUser(registerationInfo) {
      try {
        await this.$axios.post('/auth/register', registerationInfo)
        await this.$auth.loginWith('local', {
          data: registerationInfo,
        })
        // debugger
        this.$store.dispatch('snackbar/setSnackbar', {
          text: `Thanks for signing up, ${this.$auth.user.name}`,
        })
        this.$router.push('/')
      } catch (error) {
        this.$store.dispatch('snackbar/setSnackbar', {
          color: 'red',
          text: 'There was an issue signing up, please try again',
        })
      }
    },
  },
}
</script>

<style lang="scss" scoped>
</style>