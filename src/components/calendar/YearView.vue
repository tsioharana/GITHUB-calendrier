<template>
  <div class="g_cadre">
    <span class="sp_block">
      <div class="cadre_fleche_g" >
        <ChevronLeftIcon class="" @click="decrementation"/>
      </div>
      <span>{{ currentYear }}</span>
      <div class="cadre_fleche_d" >
        <ChevronRightIcon class="" @click="incrementation"/>
      </div>
    </span>
  </div>
</template>

<script>
// Importation de dayjs pour la gestion des dates,
// ref pour créer une référence réactive,
// defineEmits pour définir les événements émis dans Vue,
// ChevronLeftIcon et ChevronRightIcon pour les icônes des flèches
// import dayjs from "dayjs";
// import { ref } from "vue";
// import { defineEmits } from "vue";
import { ChevronLeftIcon, ChevronRightIcon } from "@heroicons/vue/24/outline";
// import { ref, defineEmits } from 'vue';


export default {
  // Définition du nom du composant
  name: 'YearView',
  // Déclaration des composants enfants utilisés dans ce composant
  components: {
    ChevronLeftIcon,
    ChevronRightIcon
  },
  data (){
    return {
      currentYear: new Date().getFullYear(),
    };
  },
  methods: {
    incrementation()
    {
      this.currentYear++
    },
    decrementation()
    {
      this.currentYear--
    }
  }
  // Définition de la configuration initiale du composant avec Vue 3
  // setup() {
  // Définition des événements émis par ce composant
  // const yearEmit = defineEmits(["selected"]);

  // Création d'une référence réactive pour stocker l'année courante
  // const year = ref(dayjs().year());

  // Fonction pour modifier l'année en ajoutant une valeur donnée
  // function modifyYear(v) {
  //   year.value += v;
  //   yearEmit('selected', year.value);
    
  // }

  // Retourne les données et les méthodes utilisées dans le composant
//   return {
//     year,
//     modifyYear,
//     };
// }
 };
</script>




<style scoped>
.g_cadre {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}

.sp_block {
  display: flex;
  align-items: center;
  background-color: black;
  color: white;
}

.cadre_fleche_g,
.cadre_fleche_d {
  width: 15px;
  height: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  border-radius: 5px;
  margin: 0 10px;
  cursor: pointer;
  color: white;
}
</style>
