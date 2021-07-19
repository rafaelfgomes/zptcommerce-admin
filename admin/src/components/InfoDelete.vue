<template>
  <div class="text-delete">
    <p class="mb-4">Tem certeza que deseja inativar este produto?</p>
    <form>
      <div class="row mb-3">
        <label for="product-id" class="col-sm-3 col-form-label">ID</label>
        <div class="col-sm-2">
          <input type="text" class="form-control-plaintext" id="product-id" :value="product.id">
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-id" class="col-sm-3 col-form-label">Nome</label>
        <div class="col-sm-7">
          <input type="text" class="form-control-plaintext" id="product-id" disabled :value="product.name">
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-id" class="col-sm-3 col-form-label">Preço</label>
        <div class="col-sm-5">
          <input type="text" class="form-control-plaintext" id="product-id" disabled :value="product.price">
        </div>
      </div>
      <div class="row mb-3">
        <label for="product-id" class="col-sm-3 col-form-label">Quantidade</label>
        <div class="col-sm-3">
          <input type="text" class="form-control-plaintext" id="product-id" disabled :value="product.quantity">
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'InfoDelete',
  props: {
    product: Object
  }
}
</script>

<style>

</style>