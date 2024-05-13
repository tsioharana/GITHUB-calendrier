<template>
  <div class="max-w-2xl mx-auto py-16">
      <Calendar class="calendr"/>
  </div>
</template>  

<script>
import { defineAsyncComponent } from 'vue';

const Calendar = defineAsyncComponent(() => import('./components/calendar/CalendarContainer.vue'))

export default {
  components: {
    Calendar,
  },
};
</script>

<style>
/* Votre CSS ici */
.calendr{
  width: 100%;
}
</style>
