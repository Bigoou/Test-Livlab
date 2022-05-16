<template>

  <div id="app">
    <img src="./assets/logo.png" alt="" class="logo">
    <h1 class="title">Salut Livlab :)</h1>
    <div class="search">
      <input v-model="search" placeholder="Rechercher..."/>
      <button v-on:click="filtering()">Valider</button>
    </div>
    <ul>
      <li v-show="!isFiltered" class="card" v-for="i in list" :key="i">
        <p>{{i}}</p>
      </li>
      <li v-show="isFiltered" class="card" v-for="i in filteredList" :key="i">
        <p>{{i}}</p>
      </li>
    </ul> 
  </div>
  
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      search : '',
      list : ['Décathlon (H)', '110m haies (F)', '4x400m (F)', 'Poids (H)', 'France - Slovénie (Basket H)', 'Boxe - moins de 60 kg (F)', 'Canoë-kayak - K1 200m (H)', 'Omnium (H)', 'Keirin (F) Demi-finales', 'Australie - États-Unis (Football F)'],
      isFiltered : false
    }
  },
  computed: {
    filteredList() {
      var filteredList = [];
      filteredList = this.list.filter(item => + item.toLowerCase().includes(this.search.toLowerCase()));

      // J'ai pas pensé à un meilleur moyen d'ignorer les accents ^^
      if(this.search.includes('de')){
        filteredList.push('Décathlon (H)');
      }
      if(this.search.includes('oe')){
        filteredList.push('Canoë-kayak - K1 200m (H)');
      }

      return filteredList;
    }
  },
  methods: {
    filtering() {
      return this.isFiltered = true;
    }
  },
}
</script>

<style>

* {
  box-sizing: border-box;
  margin : 0;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #546bab;
  height:100vh;
  display:flex;
  flex-direction:column;
  justify-content: center;

}

.logo {
  width : 5%;
  position: absolute;
  top : 24px;
  left : 24px;
}

.title{
  color: #fff;
  margin-bottom : 2rem;
  letter-spacing: 2px;
}

.search {
  display : inline;
}



button {
margin-left : 10px;
background-color: #131862;
border: none;
padding : 10px;
color: white;
border-radius : 4px;
transition : all 0.1s ease-in-out;
}

button:hover {
background-color: #1e258e;
cursor : pointer;
}

ul {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;

}

.card {
  padding : 20px;
  margin: 10px;
  width: 200px;
  height: 200px;
  background-color: #131862;
  border-radius: 4px;
  box-shadow: 0 2px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(19, 24, 98, 0.24);
  transition: all 0.2s ease-in-out;
  color:white;
}

.card:hover{
  transform : scale(1.03, 1.03)
}

input {
  width: 30%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: none;
  border-bottom: 2px solid #2c3e50;
  background-color: #546bab;
}

input::placeholder {
  color:#2c3e50;
}

input:focus {
  outline:none;
}

</style>
