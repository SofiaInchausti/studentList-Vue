<template>
<div>
<progress id="bar" v-show="showB" :value="value" max=10> {{showB}}</progress> 
</div>
  
</template>

<script>
export default {
    name:"ProgressBar",
    props:{  
        showB:{
            type:Boolean,
        },
        value:{
            type:Number,
        }
    },
    methods:{
        enviando(){
            this.$emit("loading")
        }
    }}
</script>

<style>

</style>