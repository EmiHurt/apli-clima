
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
       @change="getbit(fecha)"
       >


       </v-date-picker>
     </v-card>
     <v-card color="blue lighten-2 font-weight-black" >
       <v-card-text class="display-1 text-xl-center ">
      <p font-weight-black> La fecha elegida es:{{diaelegido}}<br>  El precio de un bitcon es {{precio}}US$</p>
       </v-card-text>
     </v-card>
     
   </v-flex >
   
  
 </v-layout>
 
    
  </div>
</template>

<script>
import axios from "axios";
import { mapMutations } from 'vuex';


export default {
  data(){
    return{
      fecha:new Date().toISOString().substr(0,10),
      picker: '',
      minimo: "1984",
      maximo:new Date().toISOString().substr(0,10),
      diaelegido:null,
      precio:null
     
    }
  },
  methods:{
    ...mapMutations(['mostrarloading','ocultarloading']),
    async getbit(dia){
      
      
    
   
    
      try{

        this.mostrarloading({titulo:'acciendo a la informacion', color:'secondary'})
       let datos= await axios.get(`https://api.coindesk.com/v1/bpi/historical/close.json?start=${dia}&end=${dia}`)
      var asd=datos.data.bpi

      //HICE ESTE ARREGLO PORQUE AL ENTRAR AL DATO JSON DATOS.DATA.BPI ME ARROJABA LA FECHA Y EL VALOR DEL BITCON PERO DENTRO DE CORCHETES, realice este modificacion para que se vea mejor
      var myJson = JSON.stringify(asd).split(['-']);
       let arreglo= myJson[0]+"-"+myJson[1]+"-"+myJson[2]
       
      
      
      
      

     
     
  
     this.diaelegido=  await arreglo[2]+arreglo[3]+arreglo[4]+arreglo[5]+arreglo[6]+arreglo[7]+arreglo[8]+arreglo[9]+arreglo[10]+arreglo[11]
     this.precio= await arreglo[13]+arreglo[14]+arreglo[15]+arreglo[16]+arreglo[17]
     
     
       
         

    
 
    
     
  
  
      

     


     }catch(error){
       console.log(error);
     }
     finally{
       this.ocultarloading()

     }
      
      
      

    }
  },
  created(){
    this.getbit(this.fecha)
  }
  
}
</script>
