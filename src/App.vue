<template>
  <HeaderComponent :show="show" @isShow="isShow"/>
  <main>
    
        <SearchBar v-model="search"
        @searchPokemon="fetchPokemon"
        @addMyPokemon="capturePokemon"
        @relMyPokemon="releasePokemon"
        :pokemon="pokemon"
        :isContent="isContent"
        />
        <section class="details">
          <div class="container">
            <div class="grid">
              <PokemonDetails :pokemon="pokemon" :name="namePokemon"/>
              <MyPokemons :pokemons="myPokemons" :show="show"  @viewPokemon="viewPokemon"/>
            </div >
          </div>
        </section>
      
  </main>
 

  
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import PokemonDetails from './components/PokemonDetails.vue';
import MyPokemons from './components/MyPokemons.vue';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    SearchBar,
    PokemonDetails,
    MyPokemons
  },
  data() {
    return {
      search: '',
      url: 'https://pokeapi.co/api/v2/pokemon/',
      pokemon: {},
      myPokemons: [],
      namePokemon: '',
      isContent: false,
      show: false
    }
  },
  methods: {
    fetchPokemon() {
      fetch(this.url + this.search.toLowerCase())
      .then(res => {
        if (!res.ok) {
          throw new Error(`Errore HTTP! Status: ${res.status}`);
    }
        return res.json();
      })
      .then(res => {
        const data = res;
        const types = data.types.map(type => {
        const newType = {
          name: type.type.name
        }
        return newType;
      });
        const stats = data.stats.map(stat => {
           const newStats = {
              name: stat.stat.name,
              value: stat.base_stat
            }
            return newStats;
        });
        
        const newData = {
          id: data.id,
          name: data.name,
          types: types,
          height: data.height,
          weight: data.weight,
          stats: stats,
        };
        this.pokemon = newData;
        console.log(Array.isArray(this.myPokemons));
        // if(this.myPokemons.length === 0){
        //   this.myPokemons = [];
        // }
        this.iscontentOnArray(this.pokemon, this.myPokemons)

        
    
      })
      .catch(error => {
        console.error('Errore durante la richiesta:', error.message);
        this.error()

      })
    },
    error() {
      this.namePokemon = 'No Pokémon found';
      this.pokemon = {}
    },
    viewPokemon(index) {
      this.search = this.myPokemons[index].name;
      this.fetchPokemon()
      this.isShow();
    },
    getMyPokemons() {
      if(JSON.parse(localStorage.getItem("myPokemons")).length > 0){

        this.myPokemons = JSON.parse(localStorage.getItem("myPokemons"));
      }
    },
    capturePokemon(){
      this.getMyPokemons()
      // if (this.pokemon && Array.isArray(this.myPokemons)){

        this.myPokemons.push(this.pokemon);
        
        console.log(this.myPokemons);
        localStorage.setItem("myPokemons", JSON.stringify(this.myPokemons));
        this.iscontentOnArray(this.pokemon, this.myPokemons);
        this.isShow();
      // }
      
    },
    releasePokemon() {
      this.getMyPokemons()
      this.myPokemons = this.myPokemons.filter(item => item.id !== this.pokemon.id);
      localStorage.setItem("myPokemons", JSON.stringify(this.myPokemons));
      this.iscontentOnArray(this.pokemon, this.myPokemons)
    },
    iscontentOnArray(object, arrayOfObject) {
      if(object.id !== undefined){

        this.isContent = arrayOfObject.find(obj => obj.id === object.id);
      }
    },
    isShow() {
        this.show = !this.show;
    }

  },
 
  mounted() {
    this.getMyPokemons()
    // this.myPokemons = JSON.parse(localStorage.getItem("myPokemons"));
    console.log(this.pokemon);
    this.iscontentOnArray(this.pokemon, this.myPokemons)
  }
  
}
</script>

<style lang="scss">;

@use './styles/app.scss';



.grid {
  position: relative;
  display: grid;
  width: min(calc(700px + 4rem), 100%);
  margin-inline: auto;
  // grid-template-columns: repeat(2, minmax(350px, 1fr));
  gap: 2rem;
}
</style>
