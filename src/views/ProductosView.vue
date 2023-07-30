<template>
    <div>
        Hola mundo

        <ul v-if="productos!=null">
            <li v-for="(producto,i) in productos" :key="i">
                {{producto.name}}

                <pre>AR$ {{producto.current_price}}</pre>
                
                <PrecioEnDolar :precio_producto="producto.current_price" @hizoRequest="manejadorDeRequestPrecio"/>
            </li>
        </ul>

        <div v-else>
            No hay productos
        </div>
    </div>
</template>

<script>
import PrecioEnDolar from '../components/PrecioEnDolar.vue';
export default {
    name:'Productos',
    components:{PrecioEnDolar},
    data(){
        return {
            productos: null,
            blue_price: null
        }
    },
    mounted(){
        console.log(this.$route.params);
        fetch('http://lacomarcatienda.com.ar/api/products/by/collection/'+this.$route.params.id).then((r)=>r.json()).then((data)=>{
            console.log(data);
            this.productos = data
        })
    },
    methods:{
        manejadorDeRequestPrecio(data){
            console.log('si actualizamo el precio, ahora es',data.price,'el dia:',data.date);
        }
    }
}
</script>