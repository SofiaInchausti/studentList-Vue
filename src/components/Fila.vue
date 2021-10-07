<template>
<tr>    
    <td>{{alumno.nroAlumno}}</td>
    <td>{{alumno.apellido}}</td>
    <td>{{alumno.nombre}}</td>
    <td>{{alumno.edad}}</td>
    <td>{{alumno.ciudad}}</td>
    <td>         
    <b-icon icon="pencil-fill" variant="success" @click="mandarClick('editar')" ></b-icon>
    <b-icon icon="trash-fill" variant="danger" @click="mandarClick('borrar')" ></b-icon>
    </td>
</tr>  
    
    
</template>

<script>
export default{
    name:"Fila",
    props:{
        alumno:{
            type:Object
        }
      },
    methods:{
        mandarClick(texto){
            this.$emit('onClick',{alumno:this.alumno,titulo:texto
            })
        }
    }
    

}
</script>



