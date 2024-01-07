<template>
  <div>
    <h1>Galpões Cadastrados</h1>

    <v-text-field label="Buscar Galpão" v-model="term" class="my-5"></v-text-field>

    <WarehouseTable :warehouses="filterWarehouse" />
  </div>
</template>

<script>
import Warehouse from '@/components/Warehouse.vue'
import WarehouseTable from '@/components/WarehouseTable.vue'

export default {
  name: 'WarehouseList',
  components: {
    Warehouse,
    WarehouseTable
  },
  data() {
    return {
      warehouses: [],
      term: ''
    }
  },
  async mounted() {
    this.getWarehouses()
  },
  methods: {
    async getWarehouses() {
      const response = await this.$http.get('http://localhost:3000/api/v1/warehouses')
      const result = await response.json()
      console.log(result)

      return this.warehouses = result
    }
  },
  computed: {
    filterWarehouse() {
      return this.warehouses.filter(warehouse => {
        return warehouse.name.toLowerCase().includes(this.term.toLowerCase())
      })
    }
  }
}
</script>

<style>
.form {
  margin-bottom: 20px;
}
</style>