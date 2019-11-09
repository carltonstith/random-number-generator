<template>
  <div class="home">
    <LuckyNumber />
  </div>
</template>

<script>
// @ is an alias to /src
import LuckyNumber from '@/components/LuckyNumber.vue'

export default {
  name: 'home',
  components: {
    LuckyNumber
  }
}
</script>
