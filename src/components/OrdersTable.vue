<template>
  <div class="container">
    <div>
      <Message :message="message" type="info"/>
      <table>
        <thead>
          <tr>
            <th>Nº</th>
            <th>Cliente</th>
            <th>Pão</th>
            <th>Carne</th>
            <th>Adicionais</th>
            <th>Status</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(burger, index) in burgers" :key="index">
            <td>{{burger.id}}</td>
            <td>{{burger.name}}</td>
            <td>{{burger.bread}}</td>
            <td>{{burger.meat}}</td>
            <td>
              <ul>
                <li v-for="(additional, index) in burger.additional" :key="index">
                  {{additional}}
                </li>
              </ul>
            </td>
            <td>
              <select @change="(event) => changeStatus(event, burger.id)">
                <option v-for="statusOpt in status" :key="statusOpt.id" :value="statusOpt.type" :selected="burger.status == statusOpt.type">
                  {{statusOpt.type}}
                </option>
              </select>
            </td>
            <td><button @click="() => deleteBurger(burger.id)" class="cancel">Cancelar</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue"

export default {
  components: {
    Message
  },

  data(){
    return {
      message: "",
      burgers: [],
      status: [],
    }
  },

  methods: {
    async getContent(type){
      const response = await fetch(`http://localhost:3000/${type}`)
      const data = await response.json()

      this[type] = data
    },

    async deleteBurger(id){
      const response = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: 'DELETE'
      })

      if(response.status === 200){
        this.getContent("burgers")

        this.message = `Pedido nº ${id} cancelado com sucesso.`
      }
    },

    async changeStatus(event, id){
      const status = event.target.value

      const data = JSON.stringify({ status })

      const response = await fetch(`http://localhost:3000/burgers/${id}`, {
        headers: { 'Content-Type': 'application/json' },
        method: "PATCH",
        body: data
      })

      if(response.status === 200){
        this.message = `Status do pedido nº ${id} atualizado para "${status}".`
      }
    }
  },

  watch: {
    message(){
      if(this.message)
        setTimeout(() => this.message = "", 3000)
    }
  },

  mounted(){
    this.getContent("status")
    this.getContent("burgers")
  }
}
</script>

<style scoped>
.container {
    width: 100%;
    display: flex;
    justify-content: center;
}

table{
    border-collapse: collapse;
}

th{
    border-bottom: 3px solid #222;
}

th, td {
    text-align: left;
    padding: 10px 50px 10px 5px;
}

li {
    list-style-type: none;
    padding: 5px 0;
}

select{
  padding: 5px;
  color: #222;
}

.cancel{
    cursor: pointer;
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    padding: 5px 20px;
    transition: 0.2s;
}

.cancel:hover{
    opacity: 0.8;
}
</style>