<template>
  <div id="app">
    <h1>Szobrok</h1>
    <table>
      <thead>
        <tr>
          <th>Személy</th>
          <th>Magasság</th>
          <th>Ár</th>
          <th>Műveletek</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="s in statues" :key="s.id">
          <td>{{ s.person }}</td>
          <td>{{ s.height }}</td>
          <td>{{ s.price }}</td>
          <td>
            <router-link to="/editStatue">Szerkesztés</router-link>
          </td>
          <td>
            <button>Törlés</button>
          </td>
        </tr>
        <tr>
          <td colspan="3">
            <router-link to="/createStatue">Új Szobor</router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {},
  data() {
    return {
      statues: Array
    }
  },
  methods: {
    async getStatues() {
      const response = await fetch("http://127.0.0.1:8000/api/statues")
      const data = await response.json()
      this.statues = data
    }
  },
  mounted() {
    this.getStatues()
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
  margin-top: 60px;
}
</style>
