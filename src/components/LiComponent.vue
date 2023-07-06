<template>
    <li>
        {{capitalizeFirstLetter(name)}} <button class="li-button" @click="this.$emit('show',url)">Ver</button>
    </li>
</template>

<script>
export default {
    props:{
        name:null,
        url:null
    },
    mounted(){
        // this.$emit('pintado','pinte: '+this.name) Lanza evento para decir que se inicio el componente
    },
    methods:{
      capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
      }
    }
}
</script>

<style>
    ul{
        padding-left: 0;
    }
    li{
        list-style: none;
        border: 1px solid #00bd7e;
        border-radius: 6px;
        margin: 8px 0;
        padding: 4px;
    }

    button {
        background: #50807063;
        color: #00bd7e;
        border: 1px solid #00bd7e;
        border-radius: 2px;
        font-size: 0.7rem;
        cursor: pointer;
    }

    button:hover {
        background: #cfffef63;
        color: #a4ffe1;
        border: 1px solid #3fdaa7;
    }
</style>