<template>
  <h2 class="mb-2 mt-4 d-flex justify-content-center">
    <p>Novo produto</p>
  </h2>
  <div class="row mb-5 d-flex justify-content-center">
    <div class="col-sm-6">
      <div class="card mt-4">
        <div class="card-body">
          <form enctype="multipart/form-data" ref="formRegister">
            <div class="row mb-3">
              <label for="product-name" class="col-sm-3 col-form-label"
                >Nome</label
              >
              <div class="col-sm-7">
                <input
                  type="text"
                  class="form-control"
                  name="name"
                  id="product-name"
                />
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-description" class="col-sm-3 col-form-label"
                >Descrição</label
              >
              <div class="col-sm-7">
                <textarea
                  class="form-control"
                  name="description"
                  id="product-description"
                  rows="5"
                >
                </textarea>
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-image" class="col-sm-3 col-form-label"
                >Imagem</label
              >
              <div class="col-sm-7">
                <input
                  type="file"
                  name="image"
                  class="form-control"
                  id="product-image"
                  accept="image/*"
                />
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-price" class="col-sm-3 col-form-label"
                >Preço</label
              >
              <div class="col-sm-3">
                <div class="input-group mb-3">
                  <span class="input-group-text">R$</span>
                  <input
                    @keyup="onlyNumbers()"
                    type="text"
                    ref="inputPrice"
                    class="form-control"
                    name="price"
                    id="product-price"
                    aria-label="Preço do produto"
                  />
                </div>
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-quantity" class="col-sm-3 col-form-label"
                >Quantidade</label
              >
              <div class="col-sm-2">
                <input
                  type="number"
                  class="form-control"
                  name="quantity"
                  id="product-quantity"
                  min="0"
                  value="0"
                />
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-active" class="col-sm-3 col-form-label"
                >Ativo</label
              >
              <div class="col-sm-3 d-flex align-items-center">
                <div class="form-check form-switch">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    name="active"
                    id="product-active"
                  />
                </div>
              </div>
            </div>
          </form>
          <div
            class="alert alert-dismissible fade show"
            :class="[showAlert ? '' : 'd-none', alertClass]"
            role="alert"
          >
            {{ alertText }}
            <button
              type="button"
              id="btn-alert-close"
              class="btn-close"
              data-bs-dismiss="alert"
              aria-label="Fechar"
            ></button>
          </div>
          <div class="d-flex justify-content-around">
            <button
              type="button"
              @click="storeProduct()"
              class="btn btn-primary btn-register"
              :class="btnDisabled"
            >
              Cadastrar
            </button>
            <button
              type="button"
              @click="clearForm()"
              class="btn btn-warning btn-register"
            >
              Limpar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { apiUrl } from '/config'

export default {
  name: "ProductRegister",
  data () {
    return {
      alertText: '',
      alertClass: '',
      btnDisabled: '',
      showAlert: false
    }
  },
  methods: {
    async storeProduct() {
      this.btnDisabled = "disabled";
      let formData = new FormData(this.$refs.formRegister);

      const response = await fetch(`${apiUrl}/products`, {
        method: "POST",
        body: formData,
      });

      this.showAlert = true;

      if (response.status !== 201) {
        this.errorResponse("Erro ao cadastrar o produto");
        this.btnDisabled = '';
        setTimeout(() => {
          document.getElementById("btn-alert-close").click();
        }, 5000);
        return;
      }

      this.successResponse("Produto cadastrado com sucesso");
      setTimeout(() => {
        document.getElementById("btn-close").click();
      }, 4000);
      this.clearForm()
    },
    successResponse(message) {
      this.alertText = message;
      this.alertClass = "alert-success";
    },
    errorResponse(message) {
      this.alertText = message;
      this.alertClass = "alert-danger";
    },
    clearForm() {
      this.$refs.formRegister.reset()
    },
    onlyNumbers() {
      let inputPrice = this.$refs.inputPrice
      inputPrice.value = inputPrice.value.replace(/[^0-9 \\,]/, '')
    }
  },
};
</script>

<style scoped>
.btn-register {
  width: 20%;
}
</style>
