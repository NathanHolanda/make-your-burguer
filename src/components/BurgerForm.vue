<template>
  <div class="container">
    <form @submit="createBurger">
      <Message :message="message" :type="messageType"/>
      <div class="input-container">
        <label class="input-container-label" for="name"
          >Nome do cliente:
        </label>
        <input
          id="name"
          name="name"
          v-model="name"
          type="text"
          placeholder="Digite o nome do cliente"
        />
      </div>
      <div class="input-container">
        <label class="input-container-label" for="bread"
          >Tipo de pão:
        </label>
        <select id="bread" name="bread" v-model="bread" @change="changeSelectColor">
          <option value="" hidden selected disabled>
            Selecione o tipo de pão...
          </option>
          <option v-for="bread in breads" :key="bread.id" :value="bread.type">
            {{ bread.type }}
          </option>
        </select>
      </div>
      <div class="input-container">
        <label class="input-container-label" for="meat"
          >Tipo de carne:
        </label>
        <select id="meat" name="meat" v-model="meat" @change="changeSelectColor">
          <option value="" hidden selected disabled>
            Selecione o tipo de carne...
          </option>
          <option v-for="meat in meats" :key="meat.id" :value="meat.type">
            {{ meat.type }}
          </option>
        </select>
      </div>
      <div class="input-container">
        <p class="input-container-label">Adicionais:</p>
        <div class="checkbox-group">
          <div v-for="additional in all_additional" :key="additional.id" class="checkbox-container">
            <input
              type="checkbox"
              name="chosen_additional"
              v-model="chosen_additional"
              :id="additional.type"
              :value="additional.type"
            />
            <label :for="additional.type">{{ additional.type }}</label>
          </div>
        </div>
      </div>
      <div class="button-container">
        <button type="submit">Criar meu burger!</button>
      </div>
    </form>
  </div>
</template>

<script>
import Message from "./Message.vue"

export default {
  components: {
    Message
  },

  data() {
    return {
      breads: null,
      meats: null,
      all_additional: null,
      name: "",
      bread: "",
      meat: "",
      chosen_additional: [],
      status: "Solicitado",
      message: "",
      messageType: ""
    };
  },

  methods: {
    async getIngredients() {
      const response = await fetch("http://localhost:3000/ingredients");
      const data = await response.json();

      this.breads = data.breads;
      this.meats = data.meats;
      this.all_additional = data.additional;
    },

    changeSelectColor(event){
      const select = event.target;
    
      if(select.value !== "")
        select.style.color = "#333";
      else
        select.style.color = "#777";
    },

    async createBurger(event){
      event.preventDefault()

      const order = {
        name: this.name,
        bread: this.bread,
        meat: this.meat,
        additional: this.chosen_additional,
        status: this.status
      }

      const inputs = Object.values(order)
      const hasEmptyInput = inputs.some(input => input === "")

      if(hasEmptyInput){
        this.message = "ERRO: Preencha todos os campos."
        this.messageType = "error"

        setTimeout(() => this.message = "", 3000)
      }else{
        const data = JSON.stringify(order)

        const response = await fetch("http://localhost:3000/burgers", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: data
        })

        if(response.status === 201){
            const data = await response.json()

            this.name = ""
            this.bread = ""
            this.meat = ""
            this.chosen_additional.length = 0

            this.message = `Pedido nº ${data.id} realizado!`
            this.type = "success"

            setTimeout(() => this.message = "", 3000)
        }
      }
      
    }
  },

  mounted(){
    this.getIngredients();
  }
};
</script>

<style scoped>
.container {
  width: 100%;
  display: flex;
  justify-content: center;
}

form {
  margin-top: 50px;
  max-width: 400px;
  width: 100%;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 25px;
}

.input-container-label {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 10px;
  border-left: 4px solid #fcba03;
  padding: 5px 10px;
}

.input-container input,
.input-container select {
  padding: 5px 10px;
}

.checkbox-group {
  display: flex;
  flex-wrap: wrap;
}

.checkbox-container {
  width: 50%;
}

.checkbox-container label {
  font-weight: bold;
}

input[type="checkbox"] {
  margin-right: 10px;
}

.button-container {
  width: 100%;
  text-align: center;
}

.button-container button {
  cursor: pointer;
  background-color: #222;
  padding: 15px 60px;
  font-size: 1.2rem;
  border: none;
  border-radius: 5px;
  color: #fcba03;
  transition: 0.2s;
}

.button-container button:hover {
  opacity: 0.8;
}
</style>