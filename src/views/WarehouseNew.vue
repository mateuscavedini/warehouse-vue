<template>
  <div>
    <h1>Cadastrar Galpão</h1>

    <div class="container">
      <div>
        {{ msg }}
      </div>

      <form v-on:submit.prevent>
        <div class="form">
          <label for="name">Nome:</label>
          <input id="name" type="text" placeholder="Nome do Galpão" v-model="form.name">
        </div>

        <div class="form">
          <label for="code">Código:</label>
          <input id="code" type="text" placeholder="Código do Galpão" v-model="form.code">
        </div>

        <div class="form">
          <label for="address">Endereço:</label>
          <input id="address" type="text" placeholder="Endereço do Galpão" v-model="form.address">
        </div>

        <div class="form">
          <label for="city">Cidade:</label>
          <input id="city" type="text" placeholder="Cidade" v-model="form.city">
        </div>

        <div class="form">
          <label for="cep">CEP:</label>
          <input id="cep" type="text" placeholder="CEP" v-model="form.cep">
        </div>

        <div class="form">
          <label for="area">Área:</label>
          <input id="area" type="number" v-model="form.area">
        </div>

        <div class="form">
          <label for="description">Descrição:</label>
          <textarea id="description" cols="30" rows="5" v-model="form.description"></textarea>
        </div>

        <div class="form">
          <button v-on:click="postWarehouse">Cadastrar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WarehouseNew',
  data() {
    return {
      form: {
        name: null,
        code: null,
        address: null,
        city: null,
        cep: null,
        area: null,
        description: null
      },
      msg: null
    }
  },
  methods: {
    async postWarehouse() {
      try {
        await this.$http.post('http://localhost:3000/api/v1/warehouses', {
          name: this.form.name,
          code: this.form.code,
          address: this.form.address,
          city: this.form.city,
          cep: this.form.cep,
          area: this.form.area,
          description: this.form.description
        })

        this.msg = 'Cadastrado com sucesso!'
      } catch (error) {
        this.msg = 'Ops, tente novamente!'
        console.log(error)
      }
    }
  }
}
</script>

<style>
.form {
  margin-bottom: 15px;
}

.form input {
  margin: 5px;
}
</style>