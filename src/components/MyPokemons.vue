<template>
    <div class="wrapper" :class="this.show ? 'active' : ''">
        <h3 class="card-title">My Pokémon</h3>
        <div  class="card" v-for="(pokemon, index) in this.pokemons" :key="index" @click="$emit('viewPokemon', index)">
        <div class="card-details">
            <p class="name">{{ pokemon.name }}</p>
            <div class="type">
                <span v-for="(type, i) in pokemon.types" :key="i">{{ type.name }}</span>   
            </div>
        </div>
        <img class="image" :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${pokemon.id}.svg`" :alt="pokemon.name">
        </div>

    </div>
</template>

<script>
    export default {
        props: {
            pokemons: Array,
            show: Boolean
        },
        emit: ['viewPokemon']
    }
</script>

<style lang="scss" scoped>
@use '../styles/partials/variables' as *;
.wrapper {
    position: absolute;
    inset: 0;
    transform: translateX(110%);
    width: min(350px, 100%);
    background-color: $light-blue;
    outline: 0.5rem solid #FFF;
    padding: 0.25rem;
    border-radius: 1rem;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
    transition: $transition;
    &.active {
        transform: translateX(0);
    }
        .card-title {
            color: $white;
            text-align: center;
            font-size: 1.5rem;
            padding: 1rem;
        }
        .card {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background-color: $white;
            border-radius: 0.75rem;
            padding: 1rem;
            margin-bottom: 0.25rem;
            transition: $transition;
            cursor: pointer;
            // overflow: hidden;
            &:hover {
                background-color: $yellow;
                & .name {
                    color: $blue;
                }
            }
            .card-details {
                display: flex;
                flex-direction: column;
                justify-content: center;
                gap: 1rem;
                .name {
                    text-transform: capitalize;
                    color: $light-blue;
                    font-weight: 700;
                    transition: $transition;
                }
                .type {
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    gap: 0.5rem;
                    span {
                        display: block;
                        padding: 0.125rem 0.5rem;
                        background-color: $light-blue;
                        color: $white;
                        border-radius: 3rem;
                        text-transform: capitalize;
                        font-weight: 600;
                        font-size: 0.75rem;
                    }
                }

            }
            .image {
                max-height: 60px;
                transform: scale(1);
                // opacity: 0;
                transition: $transition;
                transform-origin: bottom right;
            }
        }

        .card:hover .image {
            transform: scale(1.5);
            opacity: 1;
        }
        .card:hover .name {
            color: $blue ;
        }
        
}

</style>