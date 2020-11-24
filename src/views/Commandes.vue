<template>
  <div class="all">
    <v-app-bar class="bar">
      <v-col col="1"><img src="../assets/logo.png" alt="logo" /></v-col>
      <v-col col="5"> U - Livreur</v-col>
      <v-col col="6">{{ prenom }}</v-col>
    </v-app-bar>
    <v-container>
      <v-row v-for="commande in commandes" :key="commande.id">
        <v-container>
          <v-card
            :class="[commande.statut === 3 ? 'gray' : commande.borne.color, 'testage']"
            @click="distribuer(commande.id)"
            elevation="1"
            outlined
            shaped
            style="width: 100% !important"
          >
            <v-row>
              <v-col cols="2" class="numBorne">{{ commande.borne.id }}</v-col>
              <v-col cols="5" class="d-flex align-end mb-6">{{ commande.client.civilite }} {{ commande.client.nom }} {{ commande.client.prenom }}</v-col>
              <v-col cols="5" class="numCommande">{{ commande.codeCourt }}</v-col>
            </v-row>
          </v-card>
        </v-container>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import axios from "axios"

export default {
  data() {
    return {
      commandes: [],
      prenom: "",
    }
  },
  methods: {
    distribuer(idCommande) {
      axios.get("http://" + window.location.hostname + ":3001/commandes/" + idCommande + "/preparateur/" + localStorage.id)
    },
    getDatas() {
      axios.get("http://" + window.location.hostname + ":3001/commandes/toPick").then((r) => {
        this.commandes = r.data
      })
      setTimeout(() => {
        this.getDatas()
      }, 3000)
    },
  },
  mounted() {
    this.prenom = localStorage.prenom
    this.getDatas()
  },
}
</script>

<style>
.bar {
  background-color: #0077b2 !important;
}
.all {
  height: 100% !important;
}
.numBorne {
  font-size: 300% !important;
}
.numCommande {
  font-size: 300% !important;
}
.statut-3 {
  background-color: gray !important;
}
</style>
