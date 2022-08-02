<template>


  <div id="app">

  <div class="header">
     <h1>CRYPTO WEB</h1>
  </div> 
  <div class="search">
    <input type="text" id="currencies" v-model="search" placeholder="Search Crypto Currencies..">
  </div>
    <table id="currencies-table">
      <tr>
        <th>Rank</th>
        <th>Name</th>
        <th>Price</th>
        <th>Market Cap</th>
        <th>Price/hr</th>
      </tr>
      <tr v-for="item in filter_curr" :key="item.id">
        <td>{{ item.rank }}</td>
        <td>{{ item.name }}</td>
        <td>$ {{ item.price.toFixed(2) }}</td>
        <td>{{ item.marketCap }}</td>
        <td>{{ item.priceChange1h }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "App",

  data() {
    return {
      search: '',
      info: [],
    };
  },
  mounted() {
    axios
      .get(
        "https://api.coinstats.app/public/v1/coins?skip=0&limit=20&currency=USD")
      .then((response) => (this.info = response.data.coins));
  },
  computed: {
    filter_curr(){      
     return this.info.filter(crypto => {
        return crypto.name.toLowerCase().includes(this.search.toLowerCase())
     })
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  background-color: #73e2a7;
}
table {
  margin: auto;
  padding: 50px;
  text-align: left;
}

th{
  width: 23%;
  padding: 10px;
  text-align: left;
  background-color: #076c47;
  color: white;
}

tr{
  height: 23px;
  background-color: #f2f2f2;
}

#currencies {
  background-position: 10px 10px;
  background-repeat: no-repeat; 
  width: 60%;
  font-size: 14px; 
  padding: 12px 20px 12px 10px;
  border: 1px solid #ddd; 
  margin-bottom: 12px;
}

#currencies-table {
  width: 80%;
  border: 1px solid #ddd; 
  font-size: 14px; 
}

</style>
