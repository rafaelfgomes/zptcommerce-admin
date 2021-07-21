<template>
  <h2 class="mt-4 mb-4 d-flex justify-content-center">
    <p>Lista de produtos cadastrados</p>
  </h2>
  <div class="table-responsive">
    <table ref="productTable" class="table table-striped align-middle">
      <thead class="table-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Produto</th>
          <th scope="col">Descrição</th>
          <th scope="col">Preço</th>
          <th scope="col">Quantidade</th>
          <th scope="col">Status</th>
          <th scope="col">Açoes</th>
        </tr>
      </thead>
      <tbody>
        <tr :key="product.id" v-for="product in products">
          <th scope="row">{{ product.id }}</th>
          <td>{{ product.name }}</td>
          <td>{{ product.description }}</td>
          <td>R$&nbsp;{{ product.price }}</td>
          <td>{{ product.quantity }}</td>
          <td>{{ product.active ? 'ativo' : 'inativo' }}</td>
          <td>
            <Button
              @click="openModal('Editar Produto', 'Editar', 'edit', product)"
              iconClass="fas fa-edit" 
              color="blue"
              :active="true"
              data-bs-toggle="modal" 
              data-bs-target="#actionProduct" />
            <Button
              @click="openModal('Inativar Produto', 'Inativar', 'delete', product)"
              iconClass="fas fa-times-circle"
              color="red"
              :active="product.active"
              data-bs-toggle="modal" 
              data-bs-target="#actionProduct" />
          </td>
        </tr>
      </tbody>
    </table>
    <Modal
      ref="productModal"
      :title="modalTitle"
      :buttonText="modalButtonText"
      :type="modalType"
      :product="modalProduct" />
  </div>
  
</template>

<script>
import Button from './Button'
import Modal from './Modal'
import { apiUrl } from '/config'

export default {
  name: "ProductList",
  components: {
    Button,
    Modal
  },
  data () {
    return {
      modalTitle: '',
      modalButtonText: '',
      modalType: '',
      modalProduct: {},
      products: []
    }
  },
  async created () {
    this.products = await this.fetchProducts()
  },
  methods: {
    async fetchProducts() {
      const response = await fetch(`${apiUrl}/products`)
      const data = await response.json()
      return data
    },
    openModal(modalTitle, modalButtonText, modalType, modalProduct) {
      this.modalTitle = modalTitle,
      this.modalButtonText = modalButtonText,
      this.modalType = modalType,
      this.modalProduct = modalProduct
    }
  }
};
</script>

<style>
</style>