<template>
  <NavBarVue></NavBarVue>

  <v-container v-if="role == 'USER'">
    <h1>Bem Vindo {{ name }} usuario {{ role }}</h1>
  </v-container>

  <v-container v-if="role == 'ADMIN'">
    <h1>Bem Vindo {{ name }} usuario {{ role }}, nosso chefe!</h1>
  </v-container>


</template>

<script>
import NavBarVue from "@/components/NavBar.vue";
import { onBeforeMount, ref } from "vue";
import { useStore } from 'vuex';

export default {
  name: "HomeView",
  components: {
    NavBarVue,
  },
  setup() {
    let name = ref("");
    let role = ref("");
    const storeData = useStore()

    onBeforeMount(() => {
      bringData();
    });

    //funções
    async function bringData() {
      const response = await fetch(
        `http://localhost:8080/user/${localStorage.getItem("email")}`,
        {
          method: "GET",
          headers: {
            Authorization:
              "Bearer " + localStorage.getItem("token")
          },
        }
      );

      const data = await response.json();
      console.log(data);
      name.value = data.name;
      role.value = data.role;
    }

    return {
      name,
      role,
    };
  },
};
</script>
