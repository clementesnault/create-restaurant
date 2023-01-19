<style>
    h1 
    {
        text-align: center;
    }
    h2
    {
        text-align: center;
    }
</style>


<template>
    <div>
        <h1>Créer votre restaurant</h1>
    </div>

  <v-card class="ma-auto px-4 py-4">

  
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
  >
    <v-text-field
      v-model="datas.name"
      label="Nom du restaurant"
      required
    ></v-text-field>

    <v-text-field
      v-model="datas.address"
      label="Adresse"
      required
    ></v-text-field>

    <v-row>
      <v-col class="ma-auto">
        <h4>Heure d'ouverture</h4>
        <Datepicker v-model="datas.openingTime" time-picker/>
      </v-col>
      <v-col class="ma-auto">
        <h4>Heure de fermueture</h4>
        <Datepicker v-model="datas.closingTime" time-picker/>
      </v-col>
    </v-row><br/>


    <v-text-field
    
      v-model="datas.type"
      label="Type de restaurant"
      required
    ></v-text-field>


    <v-text-field
      v-model="datas.image"
      label="Lien de l'image"
      required
    ></v-text-field>

    <v-row>
      <v-col class="ma-auto" style="text-align: center">
        <v-btn
          color="success"
          class="mr-4"
          @click="validate"
          style="width:150px"
        >
          Valider
        </v-btn>

        <v-btn
          color="error"
          class="mr-4"
          @click="reset"
          style="width:150px"
        >
          Réinitialiser
        </v-btn>
      </v-col>
    </v-row>

  </v-form>
  </v-card>       
</template>


<script>
import axios from 'axios'
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';

export default {
  components: { Datepicker },
  data () {
    return {
        valid: true,
        datas: {
          name: '',
          address: '',
          openingTime: null,
          closingTime: null,
          type: '',
          image: '',
        }
      }
  },
  methods: {
    validate () {
        const { valid } = this.$refs.form.validate()

        if (valid) alert('Le formulaire est valide')

        var postData= {
          name: this.datas.name,
          address: this.datas.address,
          openingTime: new Date(((((this.datas.openingTime.hours * 60) + this.datas.openingTime.minutes) * 60) + this.datas.openingTime.seconds) * 1000).toUTCString(),
          closingTime: new Date(((((this.datas.closingTime.hours * 60) + this.datas.openingTime.minutes) * 60) + this.datas.openingTime.seconds) * 1000).toUTCString(),
          type: this.datas.type,
          image: this.datas.image,
        }

        axios.post("http://127.0.0.1:8000/restaurant/registerRestaurant", postData)
      },

    reset () {
        this.$refs.form.reset()
      },
    },
  async created() 
  {
    axios.get('http://127.0.0.1:8000/restaurant/displayRestaurant/', {
            headers: {
              "Content-Type": "application/json",
              "Access-Control-Allow-Origin": "*",
            },
          },{})  
    .then((resp)=>{
      console.log(resp)
    })
  },
}  
</script>