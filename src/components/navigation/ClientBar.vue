<template>
  <v-app-bar app color="main" dark>
    <v-toolbar-title class="font-weight-thin">
      <router-menu :menu="menu" />
      {{ this.$store.state.user.information.username }}
    </v-toolbar-title>

    <v-spacer></v-spacer>

    <search v-if="this.$vuetify.breakpoint.width > 280"></search>

    <v-spacer></v-spacer>

    <shopping-bag
      v-if="
        this.$vuetify.breakpoint.name !== 'xs' && this.$route.name === 'Store'
      "
    ></shopping-bag>

    <change-color v-if="this.$vuetify.breakpoint.name !== 'xs'"></change-color>

    <router-menu :menu="account" />
  </v-app-bar>
</template>

<script>
import ShoppingBag from "../util/ShoppingBag.vue";
import ChangeColor from "../util/ChangeColor.vue";
import RouterMenu from "./RouterMenu.vue";
import Search from "./Search.vue";
export default {
  name: "ClientBar",
  components: { ChangeColor, ShoppingBag, Search, RouterMenu },
  data: () => ({
    menuTemplate: {
      icon: "mdi-menu",
      path: [
        {
          to: "Store",
          icon: "mdi-bookshelf",
          name: "Libros",
        },
        {
          to: "News",
          icon: "mdi-seal-variant",
          name: "Novedades",
        },
        {
          to: "Story",
          icon: "mdi-script",
          name: "Historial de compras",
        },
        {
          to: "Buying",
          icon: "mdi-cart",
          name: "Compras",
        },
      ],
    },
    accountTemplate: {
      icon: "mdi-account",
      path: [
        {
          to: "Login",
          icon: "mdi-login",
          name: "Iniciar sesión",
        },
        {
          to: "Profile",
          icon: "mdi-account-cog",
          name: "Editar perfil",
        },
        {
          to: "Logout",
          icon: "mdi-close",
          name: "Cerrar sesión",
        },
      ],
    },
  }),
  computed: {
    menu() {
      let paths = { ...this.menuTemplate };
      if (this.$store.state.user.information.username == undefined) {
        paths.path.splice(2, 3);
      }
      return paths;
    },
    account() {
      let paths = { ...this.accountTemplate };
      if (this.$store.state.user.information.username == undefined) {
        paths.path.splice(1, 2);
      }
      return paths;
    },
  },
};
</script>

<style lang="css" scoped>
.fixed {
  position: fixed;
}
</style>
