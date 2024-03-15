<template>
  <v-app id="body" theme="dark">
    <v-row>
      <v-col class="d-flex align-center justify-center">
        <v-form class="w-100 d-flex flex-column align-center">
          <v-text-field
            label="Nome"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            :rules="nameRules"
            v-model="fullName"
          >
          </v-text-field>

          <v-text-field
            label="Email"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            :rules="emailRules"
            v-model="email"
          >
          </v-text-field>

          <v-text-field
            label="Confirme Email"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            :rules="emailRules"
            v-model="emailConfirmation"
          >
          </v-text-field>

          <v-text-field
            label="Senha"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            v-model="password"
            :rules="passwordRules"
          >
          </v-text-field>

          <v-text-field
            label="Confirme Senha"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            v-model="passwordConfirmation"
            :rules="passwordRules"
          >
          </v-text-field>

          <v-btn variant="outlined"> Cadastrar-se </v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    fullName: "",
    nameRules: [
      (value) => {
        if (value) return true;

        return "Digite seu nome";
      },
      (value) => {
        if (value?.length > 2) return true;

        return "Nome deve ter mais de 2 caracteres";
      },
    ],
    email: "",
    emailConfirmation: "",
    emailRules: [
      (value) => {
        if (value) return true;

        return "E-mail requerido";
      },
      (value) => {
        if (/.+@.+\..+/.test(value)) return true;

        return "E-mail inválido";
      }
    ],
    password: "",
    passwordConfirmation: "",
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
  }),
};
</script>

<style scoped>
#body {
  overflow: hidden;
  background-image: url("../assets/[universo-de-Einstein]-1080x1920.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
