<template>
  <v-item-group selected-class="bg-primary">
    <v-container>
      <h1 class="text-center">Personajes</h1>
      <br>
      <v-row>
        <v-col v-for="item in characters" :key="item.id" cols="cols" md="4">
          <v-item v-slot="{ selectedClass, toggle }">
            <v-card class="mx-auto pa-5" height="400" width="300" dark @click="openDialog(item)" color="black"
              elevation="18">

              <v-img :src="item.thumbnail.path + '.' + item.thumbnail.extension" height="330" cover>
              </v-img>


              <v-card-title class="text-center">{{ item.name }}</v-card-title>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
      <v-dialog v-model="dialog" max-width="700px" max-height="400px">
        <v-card style="border-radius: 20px">
          <v-card-title class="text-center" 
            style="font-size: 30px; font-family: Times New Roman, serif; font-weight: bold; background-color: black; color: white;">
            {{ selectedCharacter.name }}
          </v-card-title>
          <v-row no-gutters>
            <v-col cols="6">
              <v-img :src="selectedCharacter.thumbnail.path + '.' + selectedCharacter.thumbnail.extension" height="auto"
                cover>
              </v-img>
            </v-col>
            <v-col cols="6" class="d-flex align-center">
              <v-row no-gutters>
                <v-card-subtitle>
                  Descripción
                </v-card-subtitle>

                <v-card-text>
                  {{ selectedCharacter.description || 'No hay descripción para mostrar...' }}
                </v-card-text>
                <v-col>
                  <v-card-title style="font-size: 20px; font-family: Times New Roman, serif; font-weight: bold">
                    Estadisticas
                  </v-card-title>
                  <v-card-subtitle>
                    Numero de comics: {{ selectedCharacter.comics.available }}
                  </v-card-subtitle>

                  <v-card-subtitle>
                    Numero de series: {{ selectedCharacter.series.available }}
                  </v-card-subtitle>

                  <v-card-subtitle>
                    Numero de historias: {{ selectedCharacter.stories.available }}
                  </v-card-subtitle>

                  <v-card-subtitle>
                    Numero de eventos: {{ selectedCharacter.events.available }}
                  </v-card-subtitle>

                </v-col>

                <v-col>
                  <v-card-title style="font-size: 20px; font-family: Times New Roman, serif; font-weight: bold">
                    Top 3 Series
                  </v-card-title>

                  <v-card-text>
                    <li v-for="item in selectedCharacter.series.items.slice(0, 3)">
                      {{ item.name }}
                    </li>
                  <!-- </v-card-subtitle>  -->
                  </v-card-text>
                


                </v-col>


              </v-row>
            </v-col>
          </v-row>
        </v-card>
      </v-dialog>
    </v-container>
  </v-item-group>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      dialog: false,
      characters: [],
      selectedCharacter: {}

    }
  },
  mounted() {
    axios.get('https://gateway.marvel.com:443/v1/public/characters?ts=1&apikey=699987288fb2dc8a3483835fc5d27322&hash=3df1e8d77029aa53d48fc11664f3a491&limit=100')
      .then(response => {
        this.characters = response.data.data.results.filter(hero => {
          return hero.thumbnail.path != 'http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available';
        });
      })
      .catch(error => {
        console.error("Hubo un error", error);
      });
  },
  methods: {
    openDialog(item) {
      this.selectedCharacter = item;  // Guarda el personaje seleccionado
      this.dialog = true;  // Abre el v-dialog
    }
  }
};

</script>