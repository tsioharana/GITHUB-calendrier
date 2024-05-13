<template>
  <div class="g_cadre">
    <span class="sp_block">
      <div class="cadre_fleche_g" @click="decrementation">
        <ChevronLeftIcon />
      </div>
      <span>{{ months[currentMonth.getMonth()] }}</span>
      <div class="cadre_fleche_d" @click="incrementation">
        <ChevronRightIcon />
      </div>
    </span>
  </div>
</template>

<script>
import { ChevronLeftIcon, ChevronRightIcon } from "@heroicons/vue/24/outline";

export default {
  name: 'MonthView',
  components: {
    ChevronLeftIcon,
    ChevronRightIcon
  },
  data() {
    return {
      currentMonth: new Date(),
      months: [
        'Janvier', 'Février', 'Mars', 'Avril', 'Mai', 'Juin',
        'Juillet', 'Août', 'Septembre', 'Octobre', 'Novembre', 'Décembre'
      ]
    };
  },
  methods: {
    incrementation() {
      let newMonth = this.currentMonth.getMonth() + 1;
      let newYear = this.currentMonth.getFullYear();

      if (newMonth > 11) {
        newMonth = 0;
        newYear++;
      }

      this.currentMonth = new Date(newYear, newMonth);
    },
    decrementation() {
      let newMonth = this.currentMonth.getMonth() - 1;
      let newYear = this.currentMonth.getFullYear();

      if (newMonth < 0) {
        newMonth = 11;
        newYear--;
      }

      this.currentMonth = new Date(newYear, newMonth);
    }
  }
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
  background-color: rgb(104, 75, 75);
  color: rgb(255, 255, 255);
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
  color: rgb(7, 1, 1);
}
</style>
