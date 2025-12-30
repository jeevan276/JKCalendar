<script>
import Calendar from './components/Calendar.vue'
import ModeToggle from './components/ModeToggle.vue'
export default {
  components: {
    ModeToggle,
    Calendar,
  },
}
</script>

<template>
  <div class="p-10 flex flex-col items-center gap-5">
    <ModeToggle />
    <Calendar />
  </div>
</template>
