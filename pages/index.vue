<template>
  <v-item-group selected-class="bg-primary">
    <v-container>
      <v-row>
        <v-col v-for="item in characters" :key="item.id" cols="12" md="4">
          <v-item v-slot="{ selectedClass, toggle }">
            <v-card class="mx-auto p" max-width="344" dark height="200" @click="toggle">

              <v-img  :src="item.thumbnail.path + '.' + item.thumbnail.extension" height="auto" cover>
              </v-img>
              
              
            </v-card>
            <v-card-title>{{ item.name }}</v-card-title>
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