<script>
export default {
  data() {
    return {
      Days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
      currentMonth: new Date().getMonth() + 1, // 1-indexed
      currentYear: new Date().getFullYear(),
    }
  },
  computed: {
    currentMonthName() {
      return new Date(this.currentYear, this.currentMonth - 1).toLocaleString('default', {
        month: 'long',
      })
    },
  },
  methods: {
    daysOfMonth(year, month) {
      return new Date(year, month, 0).getDate()
    },
    startDate() {
      return new Date(this.currentYear, this.currentMonth - 1, 1).getDay()
    },
    next() {
      if (this.currentMonth === 12) {
        this.currentMonth = 1
        this.currentYear++
      } else {
        this.currentMonth++
      }
    },
    previous() {
      if (this.currentMonth === 1) {
        this.currentMonth = 12
        this.currentYear--
      } else {
        this.currentMonth--
      }
    },
    isToday(num) {
      const today = new Date()
      return (
        num === today.getDate() &&
        this.currentMonth === today.getMonth() + 1 &&
        this.currentYear === today.getFullYear()
      )
    },
  },
}
</script>

<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900 p-8 transition-colors duration-300">
    <div
      class="max-w-md mx-auto bg-white dark:bg-gray-800 rounded-2xl shadow-xl overflow-hidden border border-gray-200 dark:border-gray-700"
    >
      <header class="p-6 bg-amber-300 dark:bg-amber-500 text-gray-900">
        <div class="flex justify-between">
          <h1 class="text-xs uppercase tracking-widest font-bold opacity-70 mb-1">Vue Calendar</h1>
          <h6>JeevanKami</h6>
        </div>
        <div class="flex justify-between items-baseline">
          <h2 class="text-3xl font-black">{{ currentMonthName }}</h2>
          <span class="text-xl font-light opacity-80">{{ currentYear }}</span>
        </div>
      </header>

      <section class="p-6">
        <ul class="grid grid-cols-7 gap-y-4 text-center">
          <li
            v-for="day in Days"
            :key="day"
            class="text-xs font-bold text-gray-400 dark:text-gray-500 uppercase tracking-tighter"
          >
            {{ day }}
          </li>

          <li v-for="blank in startDate()" :key="'blank-' + blank"></li>

          <li v-for="num in daysOfMonth(currentYear, currentMonth)" :key="num">
            <button
              :class="[
                'w-10 h-10 flex items-center justify-center rounded-full transition-all duration-200 text-sm font-medium',
                isToday(num)
                  ? 'bg-amber-400 dark:bg-amber-500 text-white shadow-lg scale-110'
                  : 'text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700',
              ]"
            >
              {{ num }}
            </button>
          </li>
        </ul>
      </section>

      <footer
        class="flex justify-between p-4 bg-gray-50 dark:bg-gray-800/50 border-t border-gray-100 dark:border-gray-700"
      >
        <button
          @click="previous"
          class="px-4 py-2 text-sm font-bold text-gray-600 dark:text-gray-400 hover:text-amber-600 dark:hover:text-amber-400 transition-colors"
        >
          &larr; Prev
        </button>
        <button
          @click="next"
          class="px-4 py-2 text-sm font-bold text-gray-600 dark:text-gray-400 hover:text-amber-600 dark:hover:text-amber-400 transition-colors"
        >
          Next &rarr;
        </button>
      </footer>
    </div>
  </div>
</template>
