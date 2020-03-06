<template>
  <div class="home">
   <SetTimer/>
  </div>
</template>

<script>
// @ is an alias to /src
import SetTimer from '@/components/SetTimer.vue'

export default {
  name: 'Home',
  components: {
    SetTimer
  }
}
</script>
