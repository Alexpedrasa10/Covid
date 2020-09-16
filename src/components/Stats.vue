<template>
<div>
  <b-row align-content="center" class="all-stats">
    <b-col md="12" sm="12" xs="12" xl="12">
      <b-container>
        <div class="casos">
          <h1 class="title-stats">Casos totales:</h1>
          <h2 class="stats">{{cases}}</h2>
        </div>
      </b-container>
    </b-col>
    <b-col md="12" sm="12" xs="12" xl="12">
      <b-container>
        <div class="casos">
          <h1 class="title-stats"> Recuperados:</h1>
          <h2 class="stats">{{recovered}}</h2>
        </div>
      </b-container>
    </b-col>
    <b-col md="12" sm="12" xs="12" xl="12">
      <b-container>
        <div class="casos">
          <h1 class="title-stats">Activos:</h1>
          <h2 class="stats">{{active}}</h2>
        </div>
      </b-container>
    </b-col>
    <b-col md="12" sm="12" xs="12" xl="12">
      <b-container>
        <div class="casos">
          <h1 class="title-stats">Muertos:</h1>
          <h2 class="stats">{{deaths}}</h2>
        </div>
      </b-container>
    </b-col>
    <b-container>
      <p>Ultima actualización: {{fecha}}</p>
    </b-container>
  </b-row>
</div>
</template>

<script>
import axios from "axios";
export default {
    data () {
        return {
        all: null,
        cases: null,
        recovered: null,
        deaths: null,
        active: null,
        dia: 0,
        fecha: null
        }
    },
    methods: {
      async getCases(){
        let datos= await axios.get(`https://api.covid19api.com/country/argentina`)
        this.all = await datos.data
        this.dia = await datos.data.__ob__.value.length

        this.cases = await datos.data[(this.dia - 1)].Confirmed
        this.recovered = await datos.data[(this.dia - 1)].Recovered
        this.deaths = await datos.data[(this.dia - 1)].Deaths
        this.active = await datos.data[(this.dia - 1)].Active
        this.fecha = await datos.data[(this.dia - 1)].Date
      }
    },
    created() {
      this.getCases()    
      }
}
</script>

<style scoped>
.stats{
  font-family: "Impact";
  font-size: 3rem;
  font-weight: 800;
  text-align: center;
  color: #D94A3D;
}

.title-stats{
  text-transform: uppercase;
  text-align: center;
  color: #F1F1F1;
}

.casos{
  padding: .50rem;
  background: #605B57;
  width: 100%;
  margin-top: 1rem;
  justify-content: center;
}

.all-stats{
}
</style>