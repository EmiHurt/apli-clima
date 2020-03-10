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
       let datos= await axios.get("http://api.openweathermap.org/data/2.5/forecast?q=rosario&cnt=20&appid=8a56404ca39a5540d2ef81245d52acf1")
      console.log(datos.data.list[0].dt_txt=ddmmyy),
      console.log(datos.data.list[0])
      //console.log(datos)
     
         this.clima= await (datos.data.list[0].main.temp)
         

    
 
    
     
  
  
      

     


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
