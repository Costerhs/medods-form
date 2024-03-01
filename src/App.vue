<template>
  <div id="app">
    <div class="registerForm">
        <h2 v-if="registrationStep<=3">Заполните форму</h2>
        <MainInfoForm @set-data="setData" v-if="registrationStep == 1"/>
        <AddressForm @set-data="setData" v-else-if="registrationStep==2"/>
        <PasportForm @set-data="setData" v-else-if="registrationStep==3"/>
        <ModalSuccess @restart="restart" v-else/>
    </div>


  </div>
</template>

<script>
import MainInfoForm from './components/MainInfoForm.vue';
import AddressForm from './components/AddressForm.vue'
import PasportForm from './components/PasportForm.vue'
import ModalSuccess from './components/ModalSuccess.vue'
import {useVuelidate} from "@vuelidate/core"


export default {
  name: 'App',
  setup() {
    return {v$:useVuelidate()}
  },
  components: {
    MainInfoForm,AddressForm,PasportForm,ModalSuccess
  },
  data() {
    return {
      form:[],
      registrationStep:1
    }
  },
  methods: {
    setData(data) {
        this.form = [...this.form,data]; 
        this.registrationStep = this.registrationStep +1
        if (this.registrationStep == 4) {
          console.log(this.form);
        }
      },
      restart() {
        this.registrationStep = 1;
        this.form = []
      }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

body {
  font-family: 'Roboto';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: #f0f5ff;
}
.registerForm {
    background: white;
    padding: 40px 100px;
    border-radius: 20px;
    box-shadow: 0 4px 6px rgba(0.1, 0.1, 0.1, 0.1); 
}
@media (max-width:500px) {
    .registerForm {
        padding: 10px;
    }
}
</style>
