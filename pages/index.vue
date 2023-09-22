<template>
  <v-item-group selected-class="bg-primary">
    <v-container>
      <h1 class="text-center">Personajes</h1>
      <br>
      <v-row >
        <v-col v-for="item in characters" :key="item.id" cols="cols" md="4">
          <v-item v-slot="{ selectedClass, toggle }">
            <v-card class="mx-auto pa-5" height="400" width="300" dark @click="toggle" color="secundary" elevation="18">

              <v-img  :src="item.thumbnail.path + '.' + item.thumbnail.extension" height="330" cover>
              </v-img>
              
              
              <v-card-title class="text-center">{{ item.name }}</v-card-title>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
    </v-container>
  </v-item-group>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      characters: []
    }
  },
  mounted() {
    axios.get('https://gateway.marvel.com:443/v1/public/characters?ts=1&apikey=699987288fb2dc8a3483835fc5d27322&hash=3df1e8d77029aa53d48fc11664f3a491')
      .then(response => {
        this.characters = response.data.data.results;
      })
      .catch(error => {
        console.error("Hubo un error", error);
      });
  }
};

</script>