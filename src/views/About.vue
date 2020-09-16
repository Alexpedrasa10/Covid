<template>
  <div class="about">
    <Stats/>
  </div>
</template>

<script>
// @ is an alias to /src
import Stats from '@/components/Stats.vue'

export default {
  name: 'Home',
  components: {
    Stats
  }
}
</script>

<style>
.about{
  padding: 1rem;
  background: #F1F1F1;
}
</style>