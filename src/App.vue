<script>
import ModeToggle from './components/ModeToggle.vue'
export default {
  components: {
    ModeToggle,
  },
}
</script>

<template>
  <div class="p-10 flex flex-col items-center gap-10">
    <ModeToggle />
    <h1 class="mt-4 text-2xl font-bold text-foreground">The theme is currently working!</h1>
  </div>
</template>
