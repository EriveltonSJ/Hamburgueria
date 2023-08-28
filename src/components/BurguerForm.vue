<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form class="burger_form" @submit="createBurguer">
        <div class="input_container">
          <label for="nome">Nome do Cliente</label>
          <input
            type="text"
            name="nome"
            id="nome"
            v-model="nome"
            placeholder="Digite o seu nome:"
          />
        </div>
        <div class="input_container">
          <label for="pao">Escolha o pão</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="selecioneSeuPao">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>
        <div class="input_container">
          <label for="carne">Escolha a carne</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="selecioneSuaCarne">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>
        <div class="input_container">
          <div class="opcionais_container">
            <label class="opcionais_title" for="opcionais"
              >Selecione os opcionais:</label
            >
            <div
              class="checkbox_container"
              v-for="opcional in opcionaisdata"
              :key="opcional.id"
            >
              <input
                type="checkbox"
                name="opcionais"
                v-model="opcionais"
                :value="opcional.tipo"
              />
              <span>{{ opcional.tipo }}</span>
            </div>
          </div>
          <div class="input_container">
            <input
              type="submit"
              class="submit-btn"
              value="Criar meu Burguer !"
            />
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "./Message.vue";
export default {
  components: { Message },
  name: "BurguerForm",
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionaisdata;
    },
    async createBurguer(e) {
      e.preventDefault();

      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };
      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();

      // colocar uma msg de sistema

      this.msg = `Pedido Nº ${res.id} realizado com sucesso`;

      // limpar msg
      setTimeout(() => (this.msg = ""), 3000);

      // limpar os campos
      this.nome = "";
      this.carne = " ";
      this.pao = "";
      this.opcionais = "";
    },
  },
  mounted() {
    this.getIngredientes();
  },

  components: {
    Message,
  },
};
</script>

<style scoped>
.burger_form {
  max-width: 400px;
  margin: 0 auto;
}

.input_container {
  display: flex;
  flex-direction: column;
  margin-top: 25px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03d6;
}

.burger_form input,
select {
  padding: 5px 10px;
  width: 400px;
  border-radius: 7px;
}

.opcionais_container {
  flex-direction: row;
  flex-wrap: wrap;
}

.opcionais_title {
  width: 100%;
}

.checkbox_container {
  display: flex;
  align-items: start;
  width: 50%;
  margin-top: 20px;
  margin-left: 10px;
}

.checkbox_container span,
.checkbox_container input {
  width: auto;
}

.checkbox_container span {
  margin-left: 10px;
  font-weight: bold;
}

.submit-btn {
  background-color: #222;
  color: #fcba03d6;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.7s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
