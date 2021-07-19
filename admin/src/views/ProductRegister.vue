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
              <label for="product-name" class="col-sm-3 col-form-label">Nome</label>
              <div class="col-sm-7">
                <input type="text" class="form-control" name="name" id="product-name">
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-description" class="col-sm-3 col-form-label">Descrição</label>
              <div class="col-sm-7">
                <textarea class="form-control" name="description" id="product-description" rows="5">
                </textarea>
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-image" class="col-sm-3 col-form-label">Imagem</label>
              <div class="col-sm-7">
                <input type="file" name="image" class="form-control" id="product-image" accept="image/*">
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-price" class="col-sm-3 col-form-label">Preço</label>
              <div class="col-sm-4">
                <div class="input-group mb-3">
                  <span class="input-group-text">R$</span>
                  <input type="text" class="form-control" name="price" id="product-price" aria-label="Preço do produto">
                </div>
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-quantity" class="col-sm-3 col-form-label">Quantidade</label>
              <div class="col-sm-3">
                <input type="number" class="form-control" name="quantity" id="product-quantity">
              </div>
            </div>
            <div class="row mb-3">
              <label for="product-active" class="col-sm-3 col-form-label">Ativo</label>
              <div class="col-sm-3 d-flex align-items-center">
                <div class="form-check form-switch">
                    <input class="form-check-input" type="checkbox" name="active" id="product-active">
                </div>
              </div>
            </div>
          </form>
          <div class="alert alert-dismissible fade show" :class="[showAlert ? '' : 'd-none', alertClass]" role="alert">
            {{ alertText }}
            <button type="button" id="btn-alert-close" class="btn-close" data-bs-dismiss="alert" aria-label="Fechar"></button>
          </div>
          <div class="d-flex justify-content-around">
            <button type="button" class="btn btn-primary btn-register">Cadastrar</button>
            <button type="button" class="btn btn-warning btn-register">Limpar</button>
          </div>  
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
export default ({
  name: 'ProductRegister'
})
</script>

<style scoped>
  .btn-register {
    width: 20%;
  }
</style>
