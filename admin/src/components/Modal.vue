<template>
  <div class="modal fade" id="actionProduct" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="actionProductLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="actionProductLabel">{{ title }}</h5>
          <button id="btn-close" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Fechar"></button>
        </div>
        <div class="modal-body">
          <div v-if="type === 'edit'" class="content">
            <FormUpdate ref="updateComponent" :product="product" />
          </div>
          <div v-else class="content">
            <InfoDelete :product="product" />
          </div>
          <div class="alert alert-dismissible fade show" :class="[showAlert ? '' : 'd-none', alertClass]" role="alert">
            {{ alertText }}
            <button type="button" id="btn-alert-close" class="btn-close" data-bs-dismiss="alert" aria-label="Fechar"></button>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Fechar</button>
          <button type="button" @click="editOrDelete(type)" class="btn btn-primary" :class="btnDisabled">{{ buttonText }}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FormUpdate from './FormUpdate'
import InfoDelete from './InfoDelete'

export default {
  name: 'Modal',
  components: {
    FormUpdate,
    InfoDelete
  },
  data () {
    return {
      alertText: '',
      alertClass: '',
      btnDisabled: '',
      showAlert: false
    }
  },
  props: {
    title: String,
    buttonText: String,
    type: String,
    product: Object
  },
  methods: {
    editOrDelete(type) {
      if (type === 'edit') {
        return this.updateProduct()
      }

      return this.deleteProduct()
    },
    async deleteProduct() {
      const response = await fetch(
          `http://0.0.0.0:8085/api/v1/products/${this.product.id}`,
          {
            method: 'DELETE',
            headers: {
              'Content-Type': 'application/json'
            }
          }
      )

      this.showAlert = true

      if (response.status !== 200) {
        this.errorResponse('Erro ao inativar o produto')
        setTimeout(() => {
          document.getElementById('btn-alert-close').click()
        }, 5000)
        return
      }

      this.successResponse('Produto inativado com sucesso')
      
      setTimeout(() => {
        this.$parent.$forceUpdate()
        document.getElementById('btn-close').click()
      }, 4000)
    },
    async updateProduct() {
      let formData = new FormData(this.$refs.updateComponent.$refs.formUpdate)
     
      const response = await fetch(
          `http://0.0.0.0:8085/api/v1/products/${this.product.id}?_method=PUT`,
          {
            method: 'POST',
            body: formData
          }
      )

      this.showAlert = true

      if (!response.status === 200) {
        this.errorResponse('Erro ao atualizar o produto')
        setTimeout(() => {
          document.getElementById('btn-alert-close').click()
        }, 5000)
        return
      }

      this.successResponse('Produto atualizado com sucesso')
      setTimeout(() => {
        document.getElementById('btn-close').click()
      }, 4000)      
    },
    successResponse (message) {
      this.alertText = message
      this.alertClass = 'alert-success'
      this.btnDisabled = 'disabled'
    },
    errorResponse (message) {
      this.alertText = message
      this.alertClass = 'alert-danger'
    }
  }
}
</script>

<style>

</style>