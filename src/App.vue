<template class="template">
    <div class="div-main">
        <header class="header"> 
            <div class="input-group mb-3">
                <input type="text" name="" id="" placeholder="Nome ou ID do pokemon" class="form-control"  v-model="pokemonID">
                <button @click="searchPokemon" class="btn btn-primary">Procurar</button>
            </div>
        </header>

        <div class="card mb-3" v-if="Object.entries(pokemonData).length > 0" style="max-width: 540px;">
            <div class="row g-0">
                <div class="col-md-4 d-flex align-items-center">
                    <img class="img-fluid rounded-start custom-img" :src="pokemonData.sprites.front_default" :alt="pokemonData.name">
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                        <h2 class="card-title">{{ pokemonData.name }}</h2>
                        <p class="card-text" v-for="(type, index) in pokemonData.types" :key="index" :class="type.type.name"><span>{{type.type.name}}</span></p>
                        <p class="card-text" v-for="(stat, index) in pokemonData.stats" :key="index"><small>{{ stat.stat.name }}</small>: {{ stat.base_stat }}</p>
                        <p class="card-text">ID: <small>{{pokemonData.id}}</small></p>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>
  
<script>
    import {pokeapi} from "@/api/pokeapi";
    export default {
      name: 'App',
      data(){
        return{
          pokemonData:{},
          pokemonID:'',
        }
      },
      methods: {
        async searchPokemon(){
          try{
            const pokemonToFind = await fetch(`${pokeapi}/${this.pokemonID}`)
            const pokemon = await pokemonToFind.json()
            this.pokemonData = pokemon
            console.log(pokemon)
            return pokemon
          } catch(error){
            alert('Esse pokemon não existe!')
          }
        }
      }
    }
</script>

<style lang="scss">
    @import './pokemon_types.scss';
    .div-main{
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    } 
    .custom-img {
        height: 200px;
        width: 200px;
        display: block;
        margin: 0 auto;
    }   
    .normal {
    background-color: $normal;
    border-radius: 5px;
    }
    .fire {
    background-color: $fire;
    border-radius: 5px;
    }
    .water {
    background-color: $water;
    border-radius: 5px;
    }
    .grass {
    background-color: $grass;
    border-radius: 5px;
    }
    .electric {
    background-color: $electric;
    border-radius: 5px;
    }
    .ice {
    background-color: $ice;
    border-radius: 5px;
    }
    .fighting {
    background-color: $fighting;
    border-radius: 5px;
    }
    .poison {
    background-color: $poison;
    border-radius: 5px;
    }
    .ground {
    background-color: $ground;
    border-radius: 5px;
    }
    .flying {
    background-color: $flying;
    border-radius: 5px;
    }
    .psychic {
    background-color: $psychic;
    border-radius: 5px;
    }
    .bug {
    background-color: $bug;
    border-radius: 5px;
    }
    .rock {
    background-color: $rock;
    border-radius: 5px;
    }
    .ghost {
    background-color: $ghost;
    border-radius: 5px;
    }
    .dark {
    background-color: $dark;
    border-radius: 5px;
    }
    .dragon {
    background-color: $dragon;
    border-radius: 5px;
    }
    .steel {
    background-color: $steel;
    border-radius: 5px;
    }
    .fairy {
    background-color: $fairy;
    border-radius: 5px;
    }
    .row{
    background-color: rgb(132, 243, 206);
    }
    .card {
    box-shadow: 0 10px 10px 0 rgba(0, 0, 0, 0.5);
    }
    .input-group {
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.5);
    }
</style>
  