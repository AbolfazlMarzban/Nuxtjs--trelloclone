<template>
  <v-row align="center" justify="center">
    <v-col cols="12" sm="8" md="4" align="center">
      <v-card class="elevation-4 text-left px-5">
        <v-card-title class="fancy-title align-center justify-center">
          Jello
        </v-card-title>
        <v-card-text>
          <v-form>
            <v-text-field
              label="login"
              name="login"
              append-icon="mdi-account"
              type="text"
              v-model="auth.email"
            ></v-text-field>
            <v-text-field
              label="password"
              name="password"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              :type="show ? 'text' : 'password'"
              v-model="auth.password"
              @click:append="show = !show"
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions class="text-center justify-space-between">
          <v-btn class="login-button" @click="login" depressed large>
            Log in
          </v-btn>
          <v-btn class="login-button" @click="goToSignup"  depressed large>
            Sign up
          </v-btn>
        </v-card-actions>
      </v-card>
      <v-snackbar :timeout="4000" absolute bottom center v-model="snackbar">
        {{ snackbarText }}
      </v-snackbar>
    </v-col>
  </v-row>
</template>

<script>
export default {
layout: 'signin',
data(){
    return{
snackbar: false,
      show: false,
      snackbarText: 'No error message',
      auth:{
          email:'',
          password:''
      }
    }
},
methods:{
    login(){
        let that=this
this.$fire.auth.signInWithEmailAndPassword(this.auth.email, this.auth.password)
.catch(function(error){
    that.snackbarText = error.message
    that.snackbar = true
}).then((user)=>{
    $nuxt.$router.push('/')
})
    },
    goToSignup(){
      // console.log('booos')
      $nuxt.$router.push('/auth/signup')
    }
}
}
</script>

<style>
</style>