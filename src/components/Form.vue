<template>
  <div class='d-flex justify-content-center'>
    <!-- <div class="col-md-6 col-xs-12, table"> -->
    <b-form :class="['w-25','text-green','p-3',fondo, 'mb-3']">
      <!-- //deteccion de errores// -->
    <p v-if="errores.length">
    <b>Please correct the mistakes:</b>
    <ul>
       <li v-for="errores in errores" :key="errores" :errores="errores" >{{ errores }}</li>
    </ul>
    </p>
      <b-form-group label="Student number:">
        <b-form-input 
          v-model="nroAlumno"
          type="number"
          placeholder="Student number"
          required          
        ></b-form-input>
      </b-form-group>
      <b-form-group label="Name:">
        <b-form-input
         v-model="nombre"
         type="text"
         placeholder="Name"
         required
        ></b-form-input>
      </b-form-group>

      <b-form-group label="Lastname:">
        <b-form-input
         v-model="apellido"
         type="text"
         placeholder="Lastname"
         required
        ></b-form-input>
      </b-form-group>

      <b-form-group label="Age:">
        <b-form-input
          v-model="edad"
          placeholder="Age"
          type="number"
          
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group label="City:">
        <b-form-input
          v-model="ciudad"
          placeholder="City"
          type="text"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary" @click="validacion"  >Send</b-button>
      <b-button  variant="danger" @click="onReset">Cancel </b-button >
    </b-form>
  </div>
</template>

<script>
  export default {
    props:{
      filaSelec:{type:Object},      
    },
    data() {
      return {
        //trae los datos de la tabla//
          alumno_id:this.filaSelec._id,
          nroAlumno:this.filaSelec.nroAlumno,
          nombre:this.filaSelec.nombre,
          apellido:this.filaSelec.apellido,
          ciudad:this.filaSelec.ciudad,
          edad:this.filaSelec.edad,
          errores:[],
          fondo:"bg-warning",
          dataPost:{
            nroAlumno:null,
            nombre:"",
            apellido:"",
            edad:null,
            ciudad:""
            
          }
        }
    },
    
    methods: {
      enviar(event) {
        let dataPost={ 
          nroAlumno:this.nroAlumno,
            apellido:this.apellido,
            nombre:this.nombre,
            edad:this.edad,
            ciudad:this.ciudad
        }
         this.$emit('datosForm',{dataPost,alumno_id:this.alumno_id})
         event.preventDefault();
         
      },
      onReset() {
        console.log('entre on reset',this.nroAlumno)
              this.nroAlumno = null
              this.nombre = ''
              this.apellido=""
              this.edad = null
              this.ciudad = ''
              // e.preventDefault()
              //emitir this show false
              // this.show=false
             },


      validacion(e){
        e.preventDefault()    
        this.errores=[]
        if(this.nroAlumno.toString().length===6){
          this.enviar(e)
          this.onReset()
            
          }else{
            this.errores.push("el numero debe de ser de 6 digitos")
      } 
      },      
    }
  }

</script>