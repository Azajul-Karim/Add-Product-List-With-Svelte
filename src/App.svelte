<script>
  import { onMount } from "svelte";
  import AddListProduct from "./components/views/AddListProduct.svelte";
  import ListProduct from "./components/views/ListProduct.svelte";

  let products = [];
  let message = "";
  let message_type = "";

  function addNewProduct(event) {
    let { product } = event.detail;
    products = [...products, product];
    localStorage.setItem("products", JSON.stringify(products));
  }

  function showAlert(msg, msg_t) {
    message = msg;
    message_type = msg_t;
    setTimeout(() => {
      message = "";
      message_type = "";
    }, 2000);
  }

  function deleteList(event) {
    let { list_index } = event.detail;
    products.splice(list_index, 1);
    products = products;
    localStorage.setItem("products", JSON.stringify(products));
  }

  onMount(() => {
    if (localStorage.getItem("products") === null) {
      products = [];
    } else {
      products = JSON.parse(localStorage.getItem("products"));
    }
  });
</script>

<div class="container mt-4">
  {#if message}
    <div class="alert alert-{message_type}">{message}</div>
  {/if}
  <AddListProduct on:add_product={addNewProduct} addingAlert={showAlert} />
  <ListProduct on:delete_productList={deleteList} {products} />
</div>
