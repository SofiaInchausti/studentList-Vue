<template>    
<div class="home">
    <div class="cards">
      <b-row >
        <b-col cols="12" md="5">
          <b-card 
          img-src= '../assets/jose.jpg'          
          img-top
          class mb-2
          >
          <div>
          <div>Nombre:José
              </div>
              <div> Apellido:Brest 
            </div>
            <div> Edad:38 
            </div>
            <div>  Deportes:Futbol
            </div>
          </div>
         </b-card>
     </b-col>
     <b-col cols="12" md="5">
        <b-card 
        img-src="../assets/sofiaFoto.jpeg"
        img-top
       
        class= mb-2  
      >
        <div>
          <div>Nombre:Sofia 
            </div>
           <div> Apellido:Inchausti
           </div>
           <div> Edad:30  
           </div>
           <div>  Deportes:Pelota paleta
           </div>
          </div>
        </b-card>
    </b-col>
  </b-row>
    </div> 
 </div>
</template>

<script>
export default {
  name:"Cards"
}
</script>