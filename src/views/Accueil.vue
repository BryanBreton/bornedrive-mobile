<template>
  <div>
    <v-container>
      <v-row>
        Bonjour, Saisissez votre matricule pour continuer
      </v-row>
      <v-row>
        {{error}}
        <v-col>
          <v-text-field label="matricule" v-model="matricule" type="text"></v-text-field>
        </v-col>
        <v-col>
          <v-btn class="primary" @click="connexion()">Valider</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  data(){
    return{
      matricule: "",
      user: {},
      error: ""
    }
  },
  methods:{
    connexion(){
      axios.get('http://localhost:8080/preparateurs/'+this.matricule).then(res => {
        if(res.data.nom){
          this.user = res.data
          localStorage.nom = res.data.nom
          localStorage.prenom = res.data.prenom
          localStorage.id = res.data.id
          this.error = ""
          this.$router.push('Commandes')
        } else {
          this.error = "matricule inconnu"
        }
        
      })
    }
  }
}
</script>
