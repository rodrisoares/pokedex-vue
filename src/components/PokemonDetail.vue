<template>
    <div class="detail">
      <div class="detail-view" v-if="show">
        <div v-if="pokemon" class="image">
          <img :src="imageUrl + pokemon.id + '.png'" alt="">
        </div>
        <div v-if="pokemon" class="data">
          <h2>{{ pokemon.name }}</h2>
          <div class="property">
            <div class="left destaq">Experiência</div>
            <div class="right">{{ pokemon.base_experience }} XP</div>
          </div>
        
          <div class="property">
            <div class="left destaq">Altura</div>
            <div class="right">{{ pokemon.height / 10 }} m</div>
          </div>
          <div class="property">
            <div class="left  destaq">Peso</div>
            <div class="right">{{ pokemon.weight / 10 }} kg</div>
          </div>
          <h3>Pokemon Tipo</h3>
          <div class="types">
            <div class="type" 
              v-for="(value, index) in pokemon.types"
              :key="'value'+index">
              {{ value.type.name }}
            </div>
          </div>
          <h3>Habilidades</h3>
          <div class="abilities">
            <div class="ability" 
              v-for="(value, index) in pokemon.abilities"
              :key="'value'+index">
              {{ value.ability.name }}
            </div>
            <div class="right">{{pokemon.moves.map(item => ' ' + item.move.name).toString()}} .</div>
          </div>
          <div class="property">
          </div>
        </div>
        <h2 v-else> Pokémon não encontrado</h2>
        <button class="close" @click="closeDetail">Fechar</button>
      </div>
      <i v-else class="fas fa-spinner fa-spin"></i>
    </div>
</template>

<script>
  export default {
    props: [
      'pokemonUrl',
      'imageUrl'
    ],
    data: () => {
      return {
        show: false,
        pokemon: {}
      }      
    },
    methods: {
      fetchData() {
        let req = new Request(this.pokemonUrl);
        fetch(req)
          .then((resp) => {
            if(resp.status === 200)
              return resp.json();
          })
          .then((data) => {
            this.pokemon = data;
            this.show = true;
            this.scrollTop();
          })
          .catch((error) => {
            console.log(error);
          })
      },
      closeDetail() {
        this.$emit('closeDetail');
      },
      scrollTop() {
        window.scrollTo(0, 0);
      }
    },
    created() {
      this.fetchData();
    }
  }
</script>

<style scoped>
.detail {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    position: absolute;
    top: 0;
    left: 0;
    padding: 90px 10px 10px;
    width: calc(100% - 20px);
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
}
.detail-view {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: relative;
    width: 100%;
    max-width: 510px;
    padding: 50px 0 0;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 15px 30px rgba(0,0,0,.2),
    0 10px 10px rgba(0,0,0,.2);
}
.image {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: -60px;
    width: 120px;
    height: 120px;
    background-color: #ffcb04;
    border-radius: 50%;
    overflow: hidden;
    box-shadow: 0 15px 30px rgba(0,0,0,.2),
    0 10px 10px rgba(0,0,0,.2);
}

h2 {
    text-transform: capitalize;
}

.data {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-direction: column;
    width: 100%;
    margin-bottom: 40px;     
}
.property {
    width: 90%;
    max-width: 400px;
    border-bottom: 1px solid #ccc;
    margin-bottom: 10px;
}
.left { 
    float: left; 

}
.right { 
    float: right; 
}
h3 {
    width: 90%;
    max-width: 400px;
    border-bottom: 1px solid #ccc;
}

.types, .abilities {
    display: flex;
    justify-content: flex-start;
    flex-wrap: wrap;
    width: 90%;
    max-width: 400px; 
}
.type { 
    color: rgb(17, 67, 182);
}
.ability { 
    color: #C73015;     
}

.type, .ability {
    margin: 0 10px 10px 0;
    padding: 5px 10px;
    border-radius: 20px;
    font-weight: bold;
    font-size: 1rem;
    letter-spacing: 2px;
    text-transform: capitalize;
    word-wrap: none;
    word-break: keep-all;
    background-color: #ffffff;
    border: 3px solid;
}         
.close {
    outline: none;
    border: none;
    border-radius: 5px;
    background-color: #C73015;
    color: #efefef;
    padding: 10px 20px;
    margin-bottom: 20px;
    font-size: 1.2rem;
    cursor: pointer;
}
i {
    font-size: 2rem;
    color: #efefef;
}
.destaq {
    font-weight: bold;       
}
</style>
