<template>
  <div class='justify-content-center'>
    <b-button variant="success" class='mb-3 mr-2' @click="back">Back</b-button>
    <b-button variant="info" class='mb-3' @click="formVisible">Add</b-button>
    <ProgressBar @loading="progress" :value="contador" :showB="showBarra"/>
    <Tabla :alumnos="alumnos" @infoDeTabla="traerDatos" /> 
    <Form  :filaSelec="filaSelec" v-if="show" @datosForm="infoDeForm" @formLimpio="ocultarForm"/>
    </div>
</template> 
      
<script>
import Tabla  from "../components/Tabla";
import Form from "../components/Form";
import ProgressBar from "../components/ProgressBar";
  export default {
    name:"Student",
    components:{
      Tabla,
      Form,
      ProgressBar,
      },
    data(){
      return{
        alumnos:[],
        filaSelec:{},
        show:false,
        edicion:0,
        showBarra:false,
        contador:0
      };
    },
    methods:{
      //va a la ruta anterior
      back(){
        this.$router.go(-1)
      },
    //Get de tabla
      datosTabla(){
      fetch('https://phs-class-api.herokuapp.com/alumno?numeroGrupo=9',{
       method: "GET",
       headers:{
      "Content-Type": "application/json"
      },
      })
      .then((r)=>{
          r.json().then(
          (data)=>{
              this.alumnos=data.resultado;
            })
          })
      },
      //Funciones editar y borrar. El valor edicion=1 viene del click en editar
      traerDatos(e){
        if (e.titulo=="editar"){
          this.filaSelec=e.alumno;
          this.show=true;
          this.edicion=1;
        }
        else{
          fetch('https://phs-class-api.herokuapp.com/alumno/'+e.alumno._id+'?numeroGrupo=9',{
          method:'DELETE',
          headers:{"Content-Type": "application/json"},
           }).then((r)=>{
            r.json().then(
               this.datosTabla()
               )
             })
         }
        },
      //vista de formulario
      ocultarForm(){
        this.show=false;
        this.onReset()
      },
        onReset() {
        console.log('entre on reset',this.nroAlumno)
              this.nroAlumno = null
              this.nombre = ''
              this.apellido=""
              this.edad = null
              this.ciudad = ''
      },
      //funcion progress bar con llamada al get     
      progress(){
        let barra= setInterval(()=>{
          if(this.contador!=10){
            this.showBarra=true
            this.contador+=5
            
          }else{
            this.showBarra=false
            setTimeout(
            this.datosTabla(),1000)
            clearInterval(barra)
          }
          
        },2000)
    },

        
      
      //funcion post= agregar
      infoDeForm(data){
        this.show=false
        console.log(this.edicion, 'edicion')
        if (this.edicion!=1){
        fetch('https://phs-class-api.herokuapp.com/alumno?numeroGrupo=9',{
        method:'POST',
        headers:{"Content-Type": "application/json"},
        body: JSON.stringify(data.dataPost),
      }).then((r)=>{
           r.json().then(
               this.progress() 
        )
       })
       }else{
       // funcion editar=put  
        fetch('https://phs-class-api.herokuapp.com/alumno/'+data.alumno_id+'?numeroGrupo=9',{
        method:'PUT',
        headers:{"Content-Type": "application/json"},
        body: JSON.stringify(data.dataPost),
         }).then((r)=>{
           r.json().then(               
               this.progress()
         )
     })
     this.edicion=0
    }
  },
  //formulario visible con click en Agregar
      formVisible(){
        this.show=true
      },
  },
      mounted(){
        this.datosTabla();
      }
  }
  
</script>
