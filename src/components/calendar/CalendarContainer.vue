<template>
  <div class="flex space-x-5" v-bind="$attrs">
    <div class="flex flex-col">
    
      <DateCalendar/>
    </div>
    <div>
      <span class="resultat" v-if="selectedDateValue.value">{{ selectedDateValue.value }}</span>
      Vous avez sélectionné : <br/>
      {{ selectedDateValue.value }}
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs';
import { defineAsyncComponent, ref } from 'vue'

const DateCalendar = defineAsyncComponent(() => import('./DateCalendar.vue'))

export default {
  name: 'CalendarContainer',
  components: {
  
    DateCalendar,
  },
  setup() {
    const selectedDateValue = ref(dayjs());
    return {
      selectedDateValue,
    };
  },
};
</script>

<style scoped>
/* Votre CSS ici */
.resultat{
  
}
</style>
