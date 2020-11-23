<template>
  <div class="all">
    <v-app-bar class="bar">
      <v-col col="1"><img src="../assets/logo.png" alt="logo"></v-col>
      <v-col col="5"> U - Livreur</v-col>
      <v-col col="6">{{ prenom }}</v-col>
    </v-app-bar>
    <v-container>
      <v-row v-for="commande in commandes" :key="commande.id">
          <v-container>
              <v-card :class="[commande.statut === 3 ? 'gray' : commande.borne.color, 'testage']" @click="distribuer(commande.id)" elevation="1" outlined shaped style="width: 100% !important">
                <v-row>
                  <v-col cols="2" class="numBorne">{{ commande.borne.id }}</v-col>
                <v-col cols="8" class="d-flex align-end mb-6">{{ commande.client.nom }} : {{ commande.client.numeroCarte }}</v-col>
                <v-col cols="2" class="numCommande">{{ commande.id }}</v-col>
                </v-row>
                
              </v-card>
          </v-container>
          
      </v-row>
    </v-container>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data(){
    return{
      commandes: [],
      prenom : ""
    }
  },
  methods:{
    distribuer(idCommande){
        axios.get('http://localhost:3001/commandes/'+idCommande+'/preparateur/'+localStorage.id)
    },
    getDatas(){
        axios.get("http://localhost:3001/commandes/toPick").then(r => {
          this.commandes = r.data
        })
        setTimeout(() => {
            this.getDatas()
        }, 3000);
    }
  },
  mounted(){
      this.prenom = localStorage.prenom
      this.getDatas()
  }
}
</script>

<style>
.bar{
    background-color: #0077b2 !important;
}
.all{
    height: 100% !important;
}
.numBorne{
  font-size: 400% !important;
}
.numCommande{
  font-size: 400% !important;
}
.statut-3{
  background-color: gray !important;
}
</style>
