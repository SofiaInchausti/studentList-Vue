<template>
<div class="d-flex justify-content-center">  
            <div class="col-md-6 col-xs-12, table">
              <div>
              <h1>Student list</h1>
              </div>
              <table>
                <thead>
                <tr>
                  <th> Number</th>
                  <th>Lastname</th>
                  <th> Name</th>
                  <th> Age</th>
                  <th> City</th>
                  <th> Options</th>
                </tr>
                </thead>
                <tbody class="w-100 p-3">                  
                <Fila v-for ="alumno in alumnos" v-bind:key="alumno.nroAlumno" :alumno="alumno" 
                @onClick="obtenerClick"/>                
                </tbody>    
                  </table>            
          </div>     
    </div>
</template>



<script>
import Fila  from "../components/Fila";
  export default {
    name:"Tabla",
    components:{
      Fila
      
    },
    props:{
        alumnos:{type:Array}
      },
      methods:{
        obtenerClick(e){
          this.$emit("infoDeTabla",e)

        }
      }
  }
</script>

<style>
