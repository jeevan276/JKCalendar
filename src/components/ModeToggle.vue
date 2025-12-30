<script lang="ts">
import { useDark, useToggle } from '@vueuse/core'
import { Sun, Moon } from 'lucide-vue-next'
import { Button } from '@/components/ui/button'

export default {
  components: { Button, Sun, Moon },
  setup() {
    // VueUse handles the <html> class injection
    const isDark = useDark({
      selector: 'html',
      attribute: 'class',
      valueDark: 'dark',
      valueLight: '',
    })
    const toggleDark = useToggle(isDark)

    return { isDark, toggleDark }
  },
  methods: {
    handleToggle() {
      this.toggleDark()
      console.log('DOM Class List:', document.documentElement.classList.value)
    },
  },
}
</script>

<template>
  <div class="w-full bg-background text-foreground transition-colors duration-500">
    <div class="max-w-md mx-auto space-y-6">
      <Button variant="outline" size="icon" @click="handleToggle">
        <Moon v-if="!isDark" class="h-5 w-5" />
        <Sun v-else class="h-5 w-5" />
      </Button>

      <!-- <div class="space-y-2">
        <h1 class="text-3xl font-bold">Theme Switching</h1>
        <p class="text-muted-foreground">
          If the background is not changing, your index.css might not be loading.
        </p>
      </div>

      <div class="p-6 border rounded-xl bg-card text-card-foreground shadow-sm">
        <p>
          Current Mode: <strong>{{ isDark ? 'Dark' : 'Light' }}</strong>
        </p>
      </div> -->
    </div>
  </div>
</template>
