<template>
    <div class="container">
        <img alt="Pokemon logo" src="@/assets/img/pokemon_logo.svg">
        <h1>Pokedex VueJS</h1>
        <PokemonSearch 
            :apiUrl="apiUrl" 
            @setPokemonUrl="setPokemonUrl" 
        />
        <PokemonList 
            :imageUrl="imageUrl" 
            :apiUrl="apiUrl"
            @setPokemonUrl="setPokemonUrl" 
        />
        <PokemonDetail 
            v-if="showDetail"
            :pokemonUrl="pokemonUrl"
            :imageUrl="imageUrl"
            @closeDetail="closeDetail" 
        /> 
    </div>    
</template>
<script>
    import PokemonSearch from './PokemonSearch.vue';
    import PokemonList from './PokemonList.vue';
    import PokemonDetail from './PokemonDetail.vue';

    export default {
        data: () => {
            return {
                imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
                apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
                pokemonUrl: '',
                showDetail: false
            }
        },
        components: {
            PokemonSearch,
            PokemonList,
            PokemonDetail
        },
        methods: {
            setPokemonUrl(url) {
                this.pokemonUrl = url;
                this.showDetail = true;
            },
            closeDetail() {
                this.pokemonUrl = '';
                this.showDetail = false;
            }
        }
    }
</script>
<style  scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    background: radial-gradient(#ffbf0b, #e20000);
    font-family: 'Acme', arial;
    font-size: 1rem;
    font-weight: normal;
}

h1 {
    color: #efefef; 
}
    
</style>