<script>
  import LiComponent from '../components/LiComponent.vue'

  export default {
  components: { LiComponent },
    data() {
      return {
        cokemone:[],
        selected_pokemon:null,
      }
    },
    mounted(){
      fetch('https://pokeapi.co/api/v2/pokemon').then((r)=>r.json()).then((response)=>{
        this.cokemone = response.results
        console.log(this.cokemone);

        this.cokemone.push({name:"Pitto",url:"http://www.google.com"})
      })
    },
    methods:{
      // funcionquemanejacuandolopinta(event){
      //   console.log(event);
      // }

      manejar_vista_pokemon(url){
        fetch(url).then((r)=>r.json()).then((data)=>{
          // console.log(data);
          this.selected_pokemon = data


        }).catch((error)=>{
          console.error(error);
          alert("Se produjo un error al intentar mostrar el pokemon seleccionado")
        })
      }
    }
  }
</script>

<template>
  <div class="">
    <h1>Cokemone</h1>
    
    <table v-if="selected_pokemon">
      <tr>
        <td>
          <h3>{{selected_pokemon.name}}</h3>
          <b>XP Base:{{selected_pokemon.base_experience}}</b>
        </td>
        <td>
          <h3>Habilidades</h3>
          <span v-for="(item,a) in selected_pokemon.abilities" :key="a">
             {{item.ability.name}}<span v-if="a<selected_pokemon.abilities.length-1">,&nbsp;</span>
          </span>
        </td>
        <td class="text-right">
          <button>Ver ubicaciones</button>
        </td>
      </tr>
    </table>

    <ul>
      <LiComponent 
        v-for="(pokemon,i) in cokemone" 
        :key="i" 
        :name="pokemon.name" 
        :url="pokemon.url"
        @show="manejar_vista_pokemon($event)"
      />
      <!-- @pintado="funcionquemanejacuandolopinta($event)" Esto iba como atributo del LiComponent -->
    </ul>
  </div>
</template>

<style>
  table {
    width: 100%;
    border: 1px solid #41b883;
    border-radius:6px
  }

  td {
    vertical-align: top;
    padding: 4px 6px;
  }

  .text-right {
    text-align: right;
  }
</style>
