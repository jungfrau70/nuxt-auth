<template>
  <v-container>
    <h1>Login</h1>
    <UserAuthForm button-text="Login" :submit-form="loginUser" />
  </v-container>
</template>
  
<script>
import UserAuthForm from '@/components/UserAuthForm'

export default {
  components: {
    UserAuthForm,
  },
  methods: {
    async loginUser(loginInfo) {
      // await this.$auth.loginWith('local', {
      //   data: loginInfo
      // })
      // alert('You pressed a button')
      try {
        const response = await this.$auth.loginWith('local', { data: loginInfo })
        .then(response => (this.$auth.setUserToken(response.data[0].access_token, 'refreshToken')));
        console.log(response)
        debugger
        this.$store.dispatch('snackbar/setSnackbar', {
          text: `Thanks for signing in, ${this.$auth.user.name}`,
        })
        this.$router.push('/')
      } catch (error) {
        this.$store.dispatch('snackbar/setSnackbar', {
          color: 'red',
          text: 'There was an issue signing in, please try again',
        })
      }
    },
  },
  // methods: {
  //   async loginUser(loginInfo) {
  //     this.loading = true;
  //     try {
  //       const res = await this.$auth.loginWith("local", {
  //         data: loginInfo
  //       });
  //       this.loading = false;
  //       console.log(res)
  //       const user = res.data.data.user;
  //       this.$auth.setUser(user);
  //       this.$notify({
  //         group: "success",
  //         title: "Success!",
  //         text: "Welcome!"
  //       });
  //     } catch (error) {
  //       this.loading = false;
  //       this.$notify({
  //         group: "error",
  //         title: "Error!",
  //         text: error.response
  //           ? error.response.data.error
  //           : "Sorry an error occured, check your internet"
  //       });
  //     }
  //   }
  // }
}
</script>

<style lang="scss" scoped>
</style>

