<template>
<div>
  <section class="form">
    <b-container>
      <!-- Informacion personal !-->
      <label for="Nombre">Nombre</label>
      <b-form-input        
      id="name"
      class="mb-4" 
      type="text" 
      v-model="name"
      :state="nameState" 
      :disabled="disabled"
      placeholder="Ingrese nombre">
      </b-form-input>

      <label for="Apellido">Apellido</label>
      <b-form-input        
      id="lastname"
      class="mb-4" 
      type="text" 
      v-model="lastname"
      :state="lastnameState" 
      :disabled="disabled"
      placeholder="Ingrese apellido">
      </b-form-input>

      <label for="edad">Edad</label>
      <b-form-input        
      id="age"
      class="mb-4" 
      type="number" 
      v-model="age"
      :state="ageState"
      :disabled="disabled" 
      placeholder="Ingrese edad">
      </b-form-input>

      <label for="sexo">Sexo</label>
      <b-form-radio-group class="mb-4">
        <b-form-radio  v-model="sexo" :value="female">Femenino</b-form-radio>
        <b-form-radio  v-model="sexo"  :value="male">Masculino</b-form-radio>
      </b-form-radio-group>

      <!-- Sintomas !-->
      <label for="demo-sb">Ingrese su temperatura corporal</label>
      <b-form-spinbutton 
      id="temperaturaCorporal" 
      v-model="temperaturaCorporal" 
      min="32" 
      max="45"
      class="mb-4"
      :disabled="disabled"
      >
      </b-form-spinbutton>

      <label for="tos">¿Usted tiene tos?</label>
      <b-form-radio-group class="mb-4" :disabled="disabled" >
        <b-form-radio  v-model="tos" :value="valueTrue">Si</b-form-radio>
        <b-form-radio  v-model="tos" :value="valueFalse">No</b-form-radio>
      </b-form-radio-group>

      <label for="contacto">¿Usted ha estado en contacto con casos positivos?</label>
      <b-form-radio-group class="mb-4" :disabled="disabled">
        <b-form-radio v-model="contacto" :value="valueTrue" >Si</b-form-radio>
        <b-form-radio v-model="contacto" :value="valueFalse">No</b-form-radio>
      </b-form-radio-group>

      <label for="dolorCabeza">¿Usted ha tenido/tiene dolor de cabeza?</label>
      <b-form-radio-group class="mb-4" :disabled="disabled">
        <b-form-radio  v-model="dolorCabeza" :value="valueTrue">Si</b-form-radio>
        <b-form-radio  v-model="dolorCabeza" :value="valueFalse">No</b-form-radio>
      </b-form-radio-group>

      <label for="difParaRespirar">¿Usted tiene dificultad para respirar o sensación de falta de aire?</label>
      <b-form-radio-group class="mb-4" :disabled="disabled">
        <b-form-radio v-model="difParaRespirar" :value="valueTrue">Si</b-form-radio>
        <b-form-radio v-model="difParaRespirar" :value="valueFalse">No</b-form-radio>
      </b-form-radio-group>

      <b-button class="btn" @click="btnDiagnostico" variant="primary" :disabled="disabled" > Dar diagnostico </b-button>
      <h5 v-if="error == true" class="error">Complete todos los datos para recibir su diagnostico.</h5>

      <div  class="diagnostico" v-if="diagnostico == true">
        <h3 class="diagnostico-title">Diagnostico</h3>
        <h5>
          <b-avatar :badge="sintomas" :variant="colorAvatar" badge-variant="dark"></b-avatar>
          {{name}} {{lastname}} - {{age}} años <i :class="sexo"></i>
        </h5>

        <b-container>
          <!-- Sintomas !-->
          <p v-if="sintomas == 0"><i class="fas fa-shield-virus"></i> Usted no padece de ningún sintoma. </p>
          <p v-if="sintomas == 1"><i class="fas fa-virus"></i> Usted tiene {{sintomas}} sintoma. </p>
          <p v-if="sintomas >= 2"><i class="fas fa-viruses"></i> Usted tiene {{sintomas}} sintomas. </p>
          <!-- Grupo de riesgo !-->
          <p v-if="grupoRiesgo == true"><i class="fas fa-head-side-mask"></i> Usted forma parte del grupo de riesgo</p>
          <!-- Temperatura corporal !-->
          <p v-if="temperaturaCorporal <= 38"><i class="fas fa-temperature-low"></i> Su temperatura corporal es normal.</p>
          <p v-if="temperaturaCorporal >= 39"><i class="fas fa-thermometer-full"></i> Su temperatura corporal es más alta de lo normal.</p>

          <b-progress :max="max" height="2rem" :variant="colorAvatar">
            <b-progress-bar :value="sintomas" :label=" `${((sintomas / max) * 100).toFixed(2)}%`">
            </b-progress-bar>
          </b-progress>
          <p style="font-size:.90rem;"> Esta barra indica la probabilidad que hay que usted padezca de Covid-19</p>
        </b-container>

        <b-button pill variant="outline-light" @click="btnReinicio" > Resetear formulario </b-button>
      </div>

    </b-container>
  </section>
</div>
</template>

<script>
export default {
  data(){
    return{
      name:'',
      lastname: '',
      age: 0,
      grupoRiesgo: false,
      sexo: '',
      male: 'fas fa-mars',
      female:'fas fa-venus',
      temperaturaCorporal: 36,
      valueTrue: true,
      valueFalse: false,
      tos: null,
      contacto: null,
      dolorCabeza: null,
      difParaRespirar: null,
      diagnostico: false,
      disabled: false,
      sintomas: 0,
      colorAvatar: 'info',
      error: false,
      max: 5
    }
  },
  computed:{
    nameState(){
      //Valida que haya algo escrito
      if(this.name.length == 0){
        return null
      }

      //Valida que solo tenga letras
      let words = /^[A-Z]+$/i;
      var validacionName = words.test(this.name)

      return validacionName == true ? true : false
    },
    lastnameState(){
      //Valida que haya algo escrito
      if(this.lastname.length == 0){
        return null
      }

      //Valida que solo tenga letras
      let words = /^[A-Z]+$/i;
      var validacionLastname = words.test(this.lastname)

      return validacionLastname == true ? true : false
    },
    ageState(){
      //Valida que haya algo escrito
      if(this.age == 0){
        return null
      }

      //Identifica si es grupo de riesgo
      if(this.age >= 60){
        this.grupoRiesgo = true;
      }

      //Valida que sean numeros
      let numbers = /^[0-9]+$/i;
      var validacionAge = numbers.test(this.age)

      return validacionAge == true ? true : false
    }
  },
  methods:{
    btnDiagnostico: function (event) {
      if(
        this.name != '' &&
        this.lastname != '' &&
        this.edad != 0 &&
        this.tos != null &&
        this.contacto != null &
        this.difParaRespirar != null &&
        this.dolorCabeza != null
      ){

        this.diagnostico = true;
        this.error= false;
        this.disabled = true;

        //Detecta sintomas
        if(this.tos == true){
          this.sintomas++
        }
        if(this.contacto == true){
          this.sintomas++
        }
        if(this.dolorCabeza == true){
          this.sintomas++
        }
        if(this.difParaRespirar == true){
          this.sintomas++
        }
        if(this.temperaturaCorporal >= 39){
          this.sintomas++
        }

        //Color del avatar y barra dependiendo los sintomas
        if(this.sintomas >= 1){
          this.colorAvatar = 'info';
        }
        if(this.sintomas == 3){
          this.colorAvatar = 'warning';
        }
        if(this.sintomas >= 4){
          this.colorAvatar = 'danger';
        }


      }
      else{
        this.error = true;
      }
  },
  btnReinicio: function (event){
    this.name= ''
    this.lastname= ''
    this.age= 0
    this.grupoRiesgo= false
    this.sexo= ''
    this.male= 'fas fa-mars'
    this.female='fas fa-venus'
    this.temperaturaCorporal= 36
    this.tos= null
    this.contacto= null
    this.dolorCabeza= null
    this.difParaRespirar= null
    this.diagnostico= false
    this.disabled= false
    this.sintomas= 0
    this.colorAvatar= 'info'
    this.error= false
  }
}
}
</script>

<style scoped>
.form{
  margin-top: 1rem;
  background: #02735E;
  color: #F1F1F1;
  padding: 1rem;
  border-radius: .50rem;
}

.btn{
  width: 100%;
  background: #1B618C;
  color: #FFF;
}

.error{
  padding: 1rem;
  background: #D94A3D;
  color: #FFF;
  font-weight: 750;
}

.diagnostico{
  margin-top: 2rem;
  margin-bottom: 2rem;
  text-align: center;
  padding: .50rem;
  background: #025951;
}

.diagnostico-title{
  font-weight: 750;
}

.diagnostico p{
  text-align: initial;
  font-size: 1.25rem;
}
</style>