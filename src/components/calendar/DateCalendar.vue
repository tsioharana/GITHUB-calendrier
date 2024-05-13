<template>
  <div class="calendar">
    <!-- Boutons de navigation -->
    <div class="navigation">
      <button @click="prevMonth">&lt;</button>
      <h2>{{ currentMonthName }} {{ year }}</h2>
      <button @click="nextMonth">&gt;</button>
    </div>

    <!-- Jours de la semaine -->
    <div class="weekdays">
      <div v-for="day in weekdays" :key="day" class="weekday">{{ day }}</div>
    </div>

    <!-- Dates du mois courant -->
    <div class="days">
      <div v-for="day in daysInMonth" :key="`${day.day}-${day.month}-${day.year}`" :class="[
        'day',
        { 'empty': !day.day },
        { 'hovered': day.hovered },
        { 'current-date': isCurrentDate(day) } // Ajouter la classe si c'est la date courante
      ]">
        <span class="day-number">{{ day.day }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DateCalendar',
  data() {
    const date = new Date();
    const monthIndex = date.getMonth();
    const months = ['Janvier', 'Février', 'Mars', 'Avril', 'Mai', 'Juin', 'Juillet', 'Août', 'Septembre', 'Octobre', 'Novembre', 'Décembre'];
    return {
      year: date.getFullYear(),
      currentMonthIndex: monthIndex,
      currentMonthName: months[monthIndex],
      weekdays: ['Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam', 'Dim'],
      months: months,
    };
  },
  computed: {
    daysInMonth() {
      const lastDayOfMonth = new Date(this.year, this.currentMonthIndex + 1, 0).getDate();
      let days = [];

      const firstDayOfMonth = new Date(this.year, this.currentMonthIndex, 1).getDay();
      const startDay = firstDayOfMonth === 0 ? 6 : firstDayOfMonth - 1;

      const prevMonthLastDay = new Date(this.year, this.currentMonthIndex, 0).getDate();
      const startDayPrevMonth = prevMonthLastDay - startDay + 1;
      for (let i = startDayPrevMonth; i <= prevMonthLastDay; i++) {
        days.push({ day: '', month: this.currentMonthIndex - 1, year: this.year });
      }

      for (let i = 1; i <= lastDayOfMonth; i++) {
        days.push({ day: i, month: this.currentMonthIndex, year: this.year });
      }

      const daysNeeded = 35 - days.length;
      for (let i = 1; i <= daysNeeded; i++) {
        days.push({ day: '', month: this.currentMonthIndex + 1, year: this.year });
      }

      return days;
    }
  },
  methods: {
    prevMonth() {
      if (this.currentMonthIndex > 0) {
        this.currentMonthIndex--;
      } else {
        this.currentMonthIndex = 11;
        this.year--;
      }
      this.currentMonthName = this.months[this.currentMonthIndex];
    },
    nextMonth() {
      if (this.currentMonthIndex < 11) {
        this.currentMonthIndex++;
      } else {
        this.currentMonthIndex = 0;
        this.year++;
      }
      this.currentMonthName = this.months[this.currentMonthIndex];
    },

    isWeekend(day) {
      const date = new Date(this.year, this.currentMonthIndex, day);
      const weekday = date.getDay();
      return weekday === 0 || weekday === 6;
    },
    isCurrentDate(day) {
      const currentDate = new Date();
      return day.day === currentDate.getDate() &&
        this.currentMonthIndex === currentDate.getMonth() &&
        this.year === currentDate.getFullYear();
    }
  }
};
</script>

<style lang="css" scoped>
.calendar {
  font-family: Arial, sans-serif;
  width: 30%;
  margin: 20px auto;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  background-color: white;
}

.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.navigation h2 {
  margin: 0;
  font-size: 1.5em;
  text-align: center;
}

.navigation button {
  background: none;
  border: none;
  font-size: 1.5em;
  cursor: pointer;
  transition: color 0.3s ease;
  margin: 10px;
}

.navigation button:hover {
  color: #007bff;
}

.weekdays {
  display: flex;
  justify-content: space-between;
  padding: 10px 0;
}

.weekday {
  flex: 1;
  text-align: center;
  font-weight: bold;
  color: #555;
  padding: 10px;
}

.days {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 10px;
}

.day {
  text-align: center;
  padding: 15px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-weight: lighter;
  color: ;
}

.day .day-number {
  font-size: 0.8em;
}

/* .highlight {
  background-color: #137dad;
} */

.selected {
  background-color: #007bff;
  color: #fff;
}

.empty {
  background-color: transparent;
  color: white;
}

.current-date {
  /* border: 1px solid black; */
  border-radius: 10px;
  padding: 12px;
  background-color: #41A62A;
  color: white;
}
</style>
