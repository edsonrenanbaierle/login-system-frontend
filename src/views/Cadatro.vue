<template>
  <v-app id="body" theme="dark">
    <v-row>
      <v-col class="d-flex align-center justify-center">
        <v-form id="form" class="w-100 d-flex flex-column align-center">
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
            type="email"
          >
          </v-text-field>

          <v-text-field
            label="Confirme Email"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            :rules="emailRules"
            v-model="emailConfirmation"
            type="email"
          >
          </v-text-field>

          <v-text-field
            label="Senha"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            v-model="password"
            :rules="passwordRules"
            type="password"
          >
          </v-text-field>

          <v-text-field
            label="Confirme Senha"
            variant="outlined"
            density="compact"
            class="w-50 pb-3"
            v-model="passwordConfirmation"
            :rules="passwordRules"
            type="password"
          >
          </v-text-field>

          <p v-show="validError" id="error-message">{{ messageError }}</p>

          <v-btn @click="createUser()" variant="outlined">Cadastrar-se</v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    //variaveis
    let fullName = ref("");
    let email = ref("");
    let emailConfirmation = ref("");
    let password = ref("");
    let passwordConfirmation = ref("");
    let messageError = ref("");
    let validError = ref(false);

    //rules
    let nameRules = [
      (value) => {
        if (value) return true;

        return "Digite seu nome";
      },
      (value) => {
        if (value?.length > 2) return true;

        return "Nome deve ter mais de 2 caracteres";
      },
    ];

    let emailRules = [
      (value) => {
        if (value) return true;

        return "E-mail requerido";
      },
      (value) => {
        if (/.+@.+\..+/.test(value)) return true;

        return "E-mail inválido";
      },
    ];

    let passwordRules = [
      (value) => {
        if (value) return true;

        return "Digite sua senha!";
      },
      (value) => {
        if (value.length >= 8) return true;

        return "A senha deve conter mais de 8 caracteres";
      },
    ];

    //função de criação e confirmação dos dados do formulario
    const createUser = () => {
      if (fullName.value === "") {
        messageError.value = "Por Favor prencha o seu nome!";
        validError.value = true;
      } else if (!/.+@.+\..+/.test(email.value)) {
        messageError.value =
          "Por Favor prencha o campo de email de forma correta!";
        validError.value = true;
      } else if (!/.+@.+\..+/.test(emailConfirmation.value)) {
        messageError.value =
          "Por Favor prencha o campo de confirmação do email de forma correta!";
        validError.value = true;
      } else if (password.value === "") {
        messageError.value = "Por Favor prencha o campo de senha!";
        validError.value = true;
      } else if (passwordConfirmation.value === "") {
        messageError.value =
          "Por Favor prencha o campo de confirmação de senha!";
        validError.value = true;
      } else if (email.value !== emailConfirmation.value) {
        messageError.value = "E-mails digitados diferentes!";
        validError.value = true;
      } else if (password.value !== passwordConfirmation.value) {
        messageError.value = "Senhas não compatíveis";
        validError.value = true;
      } else {
        createUserRequest();
        clearData();
      }
    };

    async function createUserRequest() {
      const user = {
        name: fullName.value,
        email: email.value,
        password: password.value,
        role: "USER",
      };

      const data = JSON.stringify(user);

      try {
        const response = await fetch(`http://localhost:8080/user`, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: data,
        });

        if (!response.ok) {
          const erroMessageObject = JSON.parse(await response.text());

          alert(erroMessageObject.message);
        }else {
          alert("Usuario cadastrado com sucesso")
        }


      } catch (error) {
        alert("Erro durante a solicitação:", error.message);
      }
    }

    //função de limpar e resetar o formulário
    const clearData = () => {
      validError.value = false;
      const form = document.getElementById("form");
      form.reset();
      fullName.value = "";
      email.value = "";
      emailConfirmation.value = "";
      password.value = "";
      passwordConfirmation.value = "";
      messageError.value = "";
    };

    //retorno para ser possivel utilização das variaveis
    return {
      passwordRules,
      emailRules,
      nameRules,
      fullName,
      password,
      passwordConfirmation,
      email,
      emailConfirmation,
      messageError,
      validError,
      createUser,
    };
  },
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

#error-message {
  background: white;
  color: red;
  border-radius: 10px;
  padding: 5px;
  margin-bottom: 1rem;
  font-size: 0.8rem;
}
</style>
import { presets } from "babel.config";
