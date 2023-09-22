<template>
    <v-toolbar dark prominent>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>
        <v-img src="https://1000marche.net/wp-content/uploads/2020/03/Marvel-logo.png" width="170">

        </v-img>
      </v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-export</v-icon>
      </v-btn>
    </v-toolbar>
    

</template>
<script setup>
const titleApp = ref("App de Tareas")
let likes = ref(0)

const incrementLikes = () => {
  // NOTA: Recuerda acceder al valor de la propiedad con .value
  likes.value++
}
</script>

<style>
.links {
  margin: 15px;
}
</style>