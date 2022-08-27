<script>
  import { createEventDispatcher } from "svelte";
  let fire = createEventDispatcher();
  export let product = {
    productName: "",
    price: "",
  };

  function addProduct(event) {
    event.preventDefault();
    fire("add_product", { product });

    product = {
      productName: "",
      price: "",
    };
  }
</script>

<form on:submit={(event) => addProduct(event)}>
  <label for="title"><strong>PRODUCT</strong></label>
  <div class="input-group mb-3">
    <div class="input-group-prepend">
      <span class="input-group-text">
        <i class="bi bi-cart-fill" />
      </span>
    </div>
    <input
      type="text"
      class="form-control"
      aria-label="Amount (to the nearest dollar)"
      bind:value={product.productName}
    />
  </div>
  <label for="title"><strong>PRICE</strong></label>
  <div class="input-group mb-3">
    <div class="input-group-prepend">
      <span class="input-group-text"><i class="bi bi-currency-dollar" /> </span>
    </div>
    <input
      type="number"
      class="form-control"
      aria-label="Amount (to the nearest dollar)"
      bind:value={product.price}
    />
  </div>
  <br />
  <input type="submit" value="ADD" class="btn btn-dark btn-block" />
  <br />
</form>
