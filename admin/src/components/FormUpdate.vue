<template>
  <div class="form-update">
    <form enctype="multipart/form-data" ref="formUpdate">
      <div class="row mb-3">
        <label for="product-id" class="col-sm-3 col-form-label">Nome</label>
        <div class="col-sm-7">
          <input type="text" class="form-control" name="name" id="product-id" :value="product.name">
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-description" class="col-sm-3 col-form-label">Descrição</label>
        <div class="col-sm-7">
          <textarea class="form-control" name="description" id="product-description" rows="5" :value="product.description">
          </textarea>
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-image" class="col-sm-3 col-form-label">Imagem</label>
        <div class="col-sm-7">
          <img class="product-image" :src="product.image">
          <input type="file" name="image" class="form-control" id="product-image" accept="image/*">
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-price" class="col-sm-3 col-form-label">Preço</label>
        <div class="col-sm-4">
          <div class="input-group mb-3">
            <span class="input-group-text">R$</span>
            <input type="text" class="form-control" name="price" id="product-price" :value="product.price" aria-label="Preço do produto">
          </div>
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-quantity" class="col-sm-3 col-form-label">Quantidade</label>
        <div class="col-sm-3">
          <input type="number" class="form-control" name="quantity" id="product-quantity" :value="product.quantity">
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-active" class="col-sm-3 col-form-label">Ativo</label>
        <div class="col-sm-3 d-flex align-items-center">
          <div class="form-check form-switch">
              <input class="form-check-input" type="checkbox" name="active" id="product-active" :checked="product.active">
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'FormUpdate',
  props: {
    product: Object
  }
}
</script>

<style>

  .product-image {
    width: 120px;
    height: 120px;
  }

</style>