<template>
    <section class="search">
        <div class="container relative">
           
            <div class="search-wrapper">
                <input
                :value="modelValue"
                @input="$emit('update:modelValue', $event.target.value,)"
                @keyup.enter="$emit('searchPokemon')"
                @focus="$emit('showSuggestions')"
               
                
              />
              
                <ul v-if="this.showSuggestions" >
                <li v-for="option in filteredOptions" :key="option" @click="$emit('selectedPokemon', option)">
                    {{ option }}
                </li>
                </ul>
                <button @click="$emit('searchPokemon')">
                    <img src="../assets/search.svg" alt="">
                </button>
            </div>
            <div class="buttons" v-if="this.pokemon.id">
                <button @click="$emit('addMyPokemon')"  v-if="!isContent">Capture</button>
                <button @click="$emit('relMyPokemon')" v-else>Release</button>
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        props: ['modelValue', 'pokemon', 'isContent', 'options', 'showSuggestions'],
        emits: ['update:modelValue', 'searchPokemon', 'addMyPokemon', 'relMyPokemon', 'isShow', 'hideSuggestions', 'showSuggestions', 'selectedPokemon'],
        data() {
            return {
                selected: '',
            }
        },
        methods: {
            
     
            selectedPokemon() {
               
                console.log('ciao');
            }
        },

        computed: {
            filteredOptions() {
            return this.options.filter(option =>
                option.includes(this.modelValue.toLowerCase())
            );
     
            }
        },

       
    }
</script>

<style lang="scss" scoped>

@use '../styles/partials/variables' as *;
.search {
    margin-bottom: 2rem;
    .search-wrapper {
        position: relative;
        width: fit-content;
        @media (min-width: 768px) {
            margin-inline: auto;

        }
        input {
            width: 250px;
            border: 1px solid $grey;
            outline: none;
            font-size: 1rem;
            padding: 0.5rem 1rem;
            border-radius: 5rem;
            box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
            transition: $transition;
            @media (min-width: 768px) {
                padding: 1rem;
                width: 300px;
            }
            &:focus {
                border: 1px solid $blue;
            }
        }
        button {
            position: absolute;
            inset: 0.25rem 0.25rem 0.25rem auto;
            aspect-ratio: 1;
            border-radius: 50%;
            border: none;
            outline: none;
            background-color: $blue;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: $transition;
            &:hover {
                background-color: $dark-blue;
            }
            img {
                width: 1rem;
            }
        }
    }
    .buttons {
        position: absolute;
        right: 0;
        top: 0;
        button {
            display: block;
            background-color: $light-blue;
            color: $yellow;
            padding-block: 0.5rem;
            width: 70px;
            font-size: 1rem;
            font-weight: 600;
            border-radius: 3rem;
            transition: $transition;
            cursor: pointer;
            @media (min-width: 768px) {
                padding-block: 1rem;
                width: 100px;
            }
            &:hover {
                background-color: $blue;
            }
        }
    }
}
ul {
    position: absolute;
    top: calc(100% + 0.5rem);
    width: 100%;
    border-radius: 0.5rem;
    background-color: $white;
    z-index: 100;
  list-style-type: none;
  padding: 0;
  margin: 0;
  border: 1px solid #ccc;
  max-height: 150px;
  overflow-y: auto;
  &::-webkit-scrollbar {
    width: 0;
}
}

li {
  padding: 8px;
  cursor: pointer;
}

li:hover {
  background-color: #f0f0f0;
}

</style>