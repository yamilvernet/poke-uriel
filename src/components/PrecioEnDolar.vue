<template>
  <pre v-if="precio_dolar==null">U$D: <img src="@/assets/loading.gif"></pre>
  <pre v-else>U$D: {{precio_producto/precio_dolar}}</pre>
</template>

<script>
export default {
    data(){
        return {
            precio_dolar: null,

        }
    },
    props:{
        precio_producto:{
            default:0,
            type:Number
        }
    },
    mounted(){

        if(sessionStorage.getItem('precio_dolar')==null){
            fetch("https://api.bluelytics.com.ar/v2/latest").then((r)=>r.json()).then((data)=>{
                console.log('obtuve el precio',data.blue.value_avg);
    
                this.precio_dolar = data.blue.value_avg;

                sessionStorage.setItem('precio_dolar',this.precio_dolar);

                this.$emit('hizoRequest',{price:this.precio_dolar,date:Date.now()})
    
            })
        } else {
            this.precio_dolar = parseFloat(sessionStorage.getItem('precio_dolar'))
        }
    }
}
</script>

<style>

</style>