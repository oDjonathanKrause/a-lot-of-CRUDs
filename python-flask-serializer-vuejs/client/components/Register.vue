<template>
  <v-layout justify-center>
    <v-flex xs12 sm8>
      <div class="white elevation-2">
        <v-toolbar flat dense class="red darken-3" dark>
          <v-toolbar-title>Criar Conta</v-toolbar-title>
        </v-toolbar>

        <div class="pl-4 pr-4 pt-2 pb-2">

          <v-form v-model="valid">
            <v-text-field v-model="name" label="Nome" required></v-text-field>
            <v-text-field v-model="email" label="E-mail" required ></v-text-field>
            <v-text-field v-model="password" label="Senha" required ></v-text-field>
            <v-text-field v-model="store" label="Filial" required></v-text-field>
          </v-form>
        
          <div>
            <v-btn dark class="red darken-3" @click="register"> Criar Conta </v-btn>
          </div>

        </div>
      </div>
    </v-flex>
  </v-layout>
</template>
      


<script>
import AuthService from '@/services/AuthService'

export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthService.register({
          email: this.email,
          password: this.password
        })

        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>