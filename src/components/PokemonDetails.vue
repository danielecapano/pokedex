<template>
    <section class="details">
       
            <div class="wrapper">
                

                <div class="card" v-if="this.pokemon.id">

                    <div class="card-title">
                        <h3 class="name">{{ this.pokemon.name }}</h3>
                        <img  class="bg" src="../assets/pokeball.svg" alt="pokeball">
                        <img class="image" :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemon.id}.svg`" :alt="this.pokemon.name">
                    </div>
                    <div class="card-body">
                        <div class="type">
                            <span v-for="(type, i) in this.pokemon.types" :key="i">{{ type.name || 'Stat' }}</span>
                           
                        </div>
                        <p class="card-subtitle">About</p>
                        <div class="about">
                            <div class="about-info">
                                <div class="info">
                                    <img class="height" src="../assets/height.svg" alt="Height">
                                    {{ this.pokemon.height / 10 || "0.0"  }} m
                                </div>
                                <span class="name">Height</span>

                            </div>
                            <div class="about-info">
                                <div class="info">
                                    <img src="../assets/weight.svg" alt="Height">
                                    {{ (this.pokemon.weight / 10 || 0.0).toFixed(1) }} kg
                                </div>
                                <span class="name">Weight</span>
                            </div>
                        </div>
                        <p class="card-subtitle">Stats</p>
                        <div class="stats" >
                            <div class="stat" v-for="(stat, i) in this.pokemon.stats" :key="i">
                                <span class="name">{{ this.statName(stat.name) }}</span>
                                <div class="line-group">
                                    <span class="value">{{ stat.value < 100 ? '0' + stat.value : stat.value }}</span>
                                    <span class="line">
                                        <span class="line-value" :style="{width: this.calcStat(stat.value) + '%'}"></span>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    
                </div>
                <div class="card" v-else>

<div class="card-title">
    <h3 class="name">{{ this.name }}</h3>
    <img  class="bg" src="../assets/pokeball.svg" alt="pokeball">
    <img class="image" src="../assets/pokeball-image.svg" alt="Pokeball">
</div>
<div class="card-body">
    <div class="type">
        <span>Type</span>
       
    </div>
    <p class="card-subtitle">About</p>
    <div class="about">
        <div class="about-info">
            <div class="info">
                <img class="height" src="../assets/height.svg" alt="Height">
                0.0 m
            </div>
            <span class="name">Height</span>

        </div>
        <div class="about-info">
            <div class="info">
                <img src="../assets/weight.svg" alt="Height">
                0.0 kg
            </div>
            <span class="name">Weight</span>
        </div>
    </div>
    <p class="card-subtitle">Stats</p>
    <div class="stats" >
        <div class="stat">
            <span class="name">HP</span>
            <div class="line-group">
                <span class="value">000</span>
                <span class="line"></span>
            </div>
        </div>
        <div class="stat">
            <span class="name">ATK</span>
            <div class="line-group">
                <span class="value">000</span>
                <span class="line"></span>
            </div>
        </div>
        <div class="stat">
            <span class="name">DEF</span>
            <div class="line-group">
                <span class="value">000</span>
                <span class="line"></span>
            </div>
        </div>
        <div class="stat">
            <span class="name">SATK</span>
            <div class="line-group">
                <span class="value">000</span>
                <span class="line"></span>
            </div>
        </div>
        <div class="stat">
            <span class="name">SDEF</span>
            <div class="line-group">
                <span class="value">000</span>
                <span class="line"></span>
            </div>
        </div>
        <div class="stat">
            <span class="name">SDP</span>
            <div class="line-group">
                <span class="value">000</span>
                <span class="line"></span>
            </div>
        </div>

    </div>
</div>


                </div>
            </div>
       
    </section>
</template>

<script>
    export default {
        props: ['pokemon', 'name'],
        // {
        //     pokemon: {
        //         type: Object,
        //         required: true
        //     },

        // },
        methods: {
            statName(stat) {
                switch (stat) {
                    case 'hp':
                        stat =  'HP';
                        break;
                    case 'attack':
                        stat =  'ATK';
                        break;
                    case 'defense':
                        stat = 'DEF';
                        break;
                    case 'special-attack':
                    stat = 'SATK';
                        break;
                    case 'special-defense':
                    stat = 'SDEF';
                        break;
                    case 'speed':
                    stat = 'SPD';
                        break;
                }
                return stat;
            },
            calcStat(value) {
                const newValue = value / 170 * 100;
                return Math.round(newValue);
            }
        }
    }
</script>

<style lang="scss" scoped>
@use '../styles/partials/variables' as *;

.details {
    width: min(360px, 100%);
    place-items: center;
    padding-bottom: 2rem;
    // overflow: auto;
}
    
        .card {
            width: min(360px, 100%);
            height: 600px;
            background-color: $light-blue;
            border: 0.5rem solid #FFF;
            padding: 0.25rem;
            border-radius: 1.5rem;
            box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
            // overflow: auto;
            .card-title {
                position: relative;
                height: 150px;
                color: $white;
                margin-bottom: 0.25rem;
                .name {
                    text-transform: capitalize;
                    text-align: center;
                    font-size: 1.5rem;
                    padding: 1rem;
                }
                .bg {
                    position: absolute;
                    inset: 0.5rem 0.5rem 0.5rem auto;
                    max-height: calc(100% - 1rem);
                }
                .image {
                    position: absolute;
                    top: 35%;
                    left: 50%;
                    transform: translatex(-50%);
                    height: 150px;

                }
            }
            .card-body {
                background-color: $white;
                // margin: 0.25rem;
                border-radius: 0.75rem;
                padding:4rem 1rem 1rem;
                .type {
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    gap: 1rem;
                    margin-bottom: 1.5rem;
                    span {
                        display: block;
                        padding: 0.25rem 0.5rem;
                        background-color: $light-blue;
                        color: $white;
                        border-radius: 3rem;
                        text-transform: capitalize;
                        font-weight: 600;
                        font-size: 0.75rem;
                    }
                }
                .card-subtitle {
                    text-align: center;
                    font-weight: 700;
                    color: $light-blue;
                    margin-bottom: 1rem;
                }
                .about {
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    gap: 3rem;
                    margin-bottom: 2rem;
                    .about-info {
                        display: flex;
                        flex-direction: column;
                        align-items: center;
                        justify-content: center;
                        // gap: 0.5rem;
                        font-weight: 600;
                        font-size: 0.875rem;
                        .info {
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            gap: 0.25rem;
                            color: $dark-grey;
                            .height {
                                transform: rotate(90deg);
                            }
                            
                        }
                        .name {
                                color: $grey;
                                font-weight: 400;
                                font-size: 0.75rem;
                            }

                    }
                }
                .stat {
                    display: flex;
                    align-items: center;
                    gap: 1rem;
                    .name {
                        flex: 0 0 60px;
                        text-align: right;
                        font-weight: 700;
                        color: $light-blue;
                        padding: 0.25rem 0.75rem 0.25rem 0;
                        border-right: 2px solid $grey;
                        font-size: 0.875rem;
                    }
                    .line-group {
                        display: flex;
                        flex-grow: 1;
                        align-items: center;
                        gap: 0.5rem;
                        .value {
                            font-size: 0.875rem;
                            font-weight: 700;
                            color: $dark-grey;
                        }
                        .line {
                            position: relative;
                            display: block;
                            background-color: rgba($color: $light-blue, $alpha: 0.3);
                            height: 0.25rem;
                            width: 100%;
                            border-radius: 1rem;
                            .line-value {
                                position: absolute;
                                left: 0;
                                top: 0;
                                height: 100%;
                                background-color: $light-blue;
                                border-radius: 1rem;
                               
                            }
                        }

                    }
                    
                }
                
            }
        }
        // img {
        //     max-width: 150px;
        // }
//     }
    
// }

</style>