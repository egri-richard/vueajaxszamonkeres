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
            <button @click="editStatue(s)">Szerkesztés</button>
          </td>
          <td>
            <button @click="deleteStatue(s.id)">Törlés</button>
          </td>
        </tr>
        <tr>
          <td>
            <input type="text" name="person" v-model="newStatue.person" />
          </td>
          <td>
            <input type="number" name="height" v-model="newStatue.height" />
          </td>
          <td>
            <input type="number" name="price" v-model="newStatue.price" />
          </td>
          <td>
            <button @click="postStatue">Új Szobor</button>
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
      statues: Array,
      newStatue: {
        id: 0,
        person: "",
        height: 0,
        price: 0
      }
    }
  },
  methods: {
    async getStatues() {
      fetch("http://127.0.0.1:8000/api/statues")
        .then( response => response.json() )
        .then( response => this.statues = response)
    },
    async deleteStatue(id) {
      await fetch(`http://127.0.0.1:8000/api/statues/${id}`, {
        method: 'DELETE'
      })

      await this.getStatues() 
    },
    async postStatue() {
      await fetch("http://127.0.0.1:8000/api/statues", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Accept": "application/json",
        },
        body: JSON.stringify(this.newStatue)
      })

      await this.getStatues()
    },
    async editStatue()
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
