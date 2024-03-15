<template>
  <v-app id="body" class="d-flex">
    <v-row>
      <v-col
        cols="12"
        sm="12"
        md="6"
        lg="6"
        xl="6"
        class="d-flex align-center justify-center"
      >
        <v-form class="d-flex flex-column w-50 h100">
          <v-text-field
            v-model="email"
            label="Email"
            class="w-100 mb-6 cinza-claro-5"
            type="email"
            :rules="emailRules"
            required
            variant="outlined"
            density="compact"
          >
          </v-text-field>

          <v-text-field
            v-model="password"
            label="Senha"
            class="w-100 mb-10"
            type="password"
            variant="outlined"
            density="compact"
            :rules="passwordRules"
          >
          </v-text-field>

          <v-btn variant="outlined" class="w-50" location="center">
            Login
          </v-btn>

          <div class="g-signin2" data-onsuccess="onSignIn"></div>

          <p style="text-align: center">Não é cadastrado?</p>

          <router-link id="router-cadastro" to="/cadastro"
            >Clique aqui e cadastre-se!</router-link
          >
        </v-form>
      </v-col>

      <v-col id="my-app" cols="6"> </v-col>
    </v-row>
  </v-app>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
      emailRules: [
        (value) => {
          if (value) return true;

          return "Digite seu e-mail";
        },
        (value) => {
          if (/.+@.+\..+/.test(value)) return true;

          return "E-mail inválido";
        },
      ],
      passwordRules: [
        (value) => {
          if (value) return true;

          return "Digite sua senha!";
        },
        (value) => {
          if (value.length >= 8) return true;

          return "A senha deve conter mais de 8 caracteres";
        },
      ],
    };
  },
};
</script>

<style scoped>
#body {
  overflow: hidden;
  background-color: #141217;
  color: white;
}

#router-cadastro {
  text-align: center;
  font-size: 0.8rem;
  color: purple;
}

#my-app {
  background-image: url("../assets/[universo-de-Einstein]-1080x1920.jpg");
  background-size: cover;
  color: white;
  background-position: center center;
  background-size: 100%;
  background-repeat: no-repeat;
}

@media only screen and (max-width: 960px) {
  #my-app {
    display: none; /* Oculta a imagem de fundo em telas maiores ou iguais a 960px */
  }

  #body {
    background-image: url("../assets/[universo-de-Einstein]-1080x1920.jpg");
    background-size: cover;
    color: white;
    background-position: center center;
    background-size: 100%;
    background-repeat: no-repeat;
  }
}
</style>
