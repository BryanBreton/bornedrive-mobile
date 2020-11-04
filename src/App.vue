<template>
  <v-app v-if="isAuth">
    <top-bar></top-bar>
    <display-alert-button></display-alert-button>

    <v-main class="background">
      <router-view />
      <v-overlay :value="isLoading" :z-index="250"> <v-progress-circular indeterminate size="80" color="primary" :width="6"></v-progress-circular> </v-overlay>
    </v-main>

    <v-footer app class="footer-style background"> <alert></alert> </v-footer>
  </v-app>
</template>

<script>
import { mapState, mapActions } from "vuex"
import TopBar from "@/components/top-bar/TopBar"
import DisplayAlertButton from "@/components/DisplayAlertButton"
import Alert from "@/components/Alert"
export default {
  name: "App",
  components: {
    TopBar,
    DisplayAlertButton,
    Alert
  },
  computed: {
    ...mapState("commonStore", ["isAuth", "isLoading"])
  },
  methods: {
    ...mapActions("commonStore", ["launchAuthentif"])
  },
  async mounted() {
    await this.launchAuthentif()
  }
}
</script>

<style lang="scss" scoped>
.background {
  background-color: white !important;
}
.footer-style {
  z-index: 300;
  padding: 0px;
}
</style>
