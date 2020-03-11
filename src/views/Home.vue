const APIKEY="8a56404ca39a5540d2ef81245d52acf1"
<template>

<div>
 <v-layout :wrap="true">
   <v-flex xl12>
     <v-card>
       <v-date-picker 
       v-model="fecha"
       full-width=""
       locale="es-ar"
       :min="minimo"
       :max="maximo"
       @change="getClima(fecha)"
       >


       </v-date-picker>
     </v-card>
     <v-card color="blue lighten-2" dark>
       <v-card-text class="display-1 text-xl-center">
      {{clima}}
       </v-card-text>
     </v-card>
     
   </v-flex >
   
  
 </v-layout>
 
    
  </div>
</template>

<script>
import axios from "axios";

export default {
  data(){
    return{
      fecha:new Date().toISOString().substr(10,0),
      picker: '',
      minimo: "1984",
      maximo:new Date().toISOString().substr(10,0),
      clima:null
    }
  },
  methods:{
    async getClima(dia){
    
    let arrayfecha=dia.split(['-'])
    
    let ddmmyy= arrayfecha[2]+"-"+arrayfecha[1]+"-"+arrayfecha[0]
    
      try{
       let datos= await axios.get(`https://api.weatherbit.io/v2.0/forecast/daily?city=kiev,UA,days=2020-03-03&key=db9797214fa543e1a988d0df149ed8c2`)
      
     //console.log(datos.data.data[0].datatime)
     


      let temperatura=datos.data.data[0].temp
      console.log(temperatura)
      let dias=datos.data.data[0].valid_date=ddmmyy
      console.log(dias)
     
      
     
     
         this.clima= await temperatura,dias
         

    
 
    
     
  
  
      

     


     }catch(error){
       console.log(error);
     }
     finally{

     }
      
      
      

    }
  },
  created(){
    this.getClima(this.fecha)
  }
  
}
</script>
