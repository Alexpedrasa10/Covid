<template>
  <div class="home">
    <section class="home-page">
      <b-container>
        <h1 class="title-page">Formulario Covid-19</h1>
        <p>Recuerde: este diagnostico no es 100% verdadero. </p>
        <FormCovid/>
      </b-container>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import FormCovid from '@/components/Form-Covid.vue'

export default {
  name: 'Home',
  components: {
    FormCovid
  }
}
</script>

<style>
.title-page{
  font-size: 2rem;
  text-transform: uppercase;
  text-align: center;
  font-weight: 800;
}

.home-page{
  padding: 1rem;
  background: #F1F1F1;
}
</style>
