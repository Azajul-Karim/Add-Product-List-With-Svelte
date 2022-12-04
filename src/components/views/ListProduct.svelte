<script>
  import { createEventDispatcher } from "svelte";
  import DeleteButton from "../helpers/DeleteButton.svelte";
  let fire = createEventDispatcher();

  export let products = [];
  $: total = products.length
    ? products.reduce((sum, { price }) => {
        return (sum = sum + price);
      }, 0)
    : 0;

  function deleteProductList(event, index) {
    fire("delete_productList", { list_index: index });
  }

  // function createdAt() {
  //   let date = new Date();
  //   let day = date.getDate();
  //   let month = date.getMonth() + 1;
  //   let year = date.getFullYear();
  //   let time = date.toLocaleTimeString();
  //   return `${day}/${month}/${year}
  //   ${time}`;
  // }

  // function createdAt() {
  //   let newDate = new Date();
  //   let date = newDate.toLocaleDateString();
  //   let time = newDate.toLocaleTimeString();
  //   return `${date}  ${time}`;
  // }
</script>

<table class="table table-striped mt-5 text-center">
  <thead class="table table-dark">
    <tr>
      <th>Product</th>
      <th>Price</th>
      <th>Creted At</th>
      <th />
    </tr>
  </thead>
  <tbody>
    {#each products as product, i}
      <tr class="list">
        <td>{product.productName}</td>
        <td>{product.price}</td>
        <td>{product.created_date} <br /> {product.created_time}</td>
        <td class="text-right">
          <DeleteButton on:delete={(event) => deleteProductList(event, i)} />
        </td>
      </tr>
    {/each}
  </tbody>
  <thead>
    {#if products.length}
      <tr class="total">
        <td>Total</td>

        <td>{total}</td>
      </tr>
    {/if}
  </thead>
</table>
