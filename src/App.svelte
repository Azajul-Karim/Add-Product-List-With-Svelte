<script>
  import AddListProduct from "./components/AddListProduct.svelte";
  import ListProduct from "./components/ListProduct.svelte";

  let products = [];
  function addNewProduct(event) {
    let { product } = event.detail;
    products = [...products, product];
  }
</script>

<div class="container mt-4">
  <AddListProduct on:add_product={addNewProduct} />
  <ListProduct {products} />
</div>
