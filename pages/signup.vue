<template>
  <v-container>
    <h1>SignUp</h1>
    <UserAuthForm
      button-text="SignUp"
      :submit-form="signUpUser"
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
  middleware: 'guest',
  methods: {
    // async registerUser() {
    //   this.loading = true;
    //   let data = this.register;
    //   try {
    //     await this.$axios.post("/signup", data);
    //     this.$router.push("/login");
    //     this.loading = false;
    //     this.$notify({
    //       group: "success",
    //       title: "Success!",
    //       text: "Account created successfully"
    //     });
    //   } catch (error) {
    //     this.loading = false;
    //     this.$notify({
    //       group: "error",
    //       title: "Error!",
    //       text: error.response
    //         ? error.response.data.error
    //         : "Sorry an error occured, check your internet"
    //     });
    //   }
    // }
    async signUpUser(signUpInfo) {
      try {
        await this.$axios.post('/signup', signUpInfo)
        await this.$auth.loginWith('local', {
          data: signUpInfo
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