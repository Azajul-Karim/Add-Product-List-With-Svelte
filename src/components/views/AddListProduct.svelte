<script>
  import { createEventDispatcher } from "svelte";
  import SubmitButton from "../helpers/SubmitButton.svelte";
  let fire = createEventDispatcher();
  export let product = {
    productName: "",
    price: "",
  };

  export let addingAlert;

  function addProduct(event) {
    event.preventDefault();

    if (!product.productName || !product.price) {
      addingAlert("Please fill in all fields", "danger");
    } else {
      submitTracker.saving = true;
      setTimeout(() => {
        product.created_date = DateNow();
        product.created_time = TimeNow();
        fire("add_product", { product });

        product = {
          productName: "",
          price: "",
          created_date: "",
          created_time: "",
        };
        submitTracker.saving = false;
        submitTracker.saved = true;
      }, 1000);
    }
  }

  let submitTracker = {
    saving: false,
    saved: false,
  };

  function DateNow() {
    let newDate = new Date();
    return newDate.toLocaleDateString();
  }

  function TimeNow() {
    let newDate = new Date();
    return newDate.toLocaleTimeString();
  }
</script>

<form on:submit={(event) => addProduct(event)}>
  <label for="title"><strong>PRODUCT</strong></label>
  <div class="input-group mb-2">
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
  <SubmitButton tracker={submitTracker} text="Save" saved_text="Saved" />
  <br />
</form>
