<template>
  <v-dialog
    v-model="this.$store.state.shoppingBag"
    transition="dialog-top-transition"
    hide-overlay
    fullscreen
  >
    <v-card cols="12" dark>
      <div class="d-flex flex-no-wrap">
        <div>
          <v-card-title class="text-h5">Libros a comprar </v-card-title>
          <v-card-text class="bagContainer">
            <bag />
          </v-card-text>

          <v-card-actions>
            <v-btn
              dark
              small
              rounded
              class="ml-2"
              color="alert"
              @click="sendBill"
            >
              Comprar
            </v-btn>

            <v-btn
              dark
              small
              rounded
              class="ml-2"
              color="signs"
              @click="closeBag"
            >
              Cerrar
            </v-btn>
          </v-card-actions>
        </div>
      </div>
    </v-card>
  </v-dialog>
</template>

<script>
import Bag from "../buying/Bag.vue";
export default {
  name: "ShoppingBagLayout",
  components: { Bag },
  methods: {
    sendBill() {
      this.$router.push({ name: "Buying" }).catch(() => {
        console.log("Buying");
      });
    },
    closeBag() {
      this.$store.dispatch("changeShoppingBag", !this.$store.state.shoppingBag);
    },
  },
};
</script>

<style lang="css" scoped>
.bagContainer {
  max-height: 80vh;
}
</style>
