<script>
  export let products = [];
  $: total = products.length
    ? products.reduce((sum, { price }) => {
        return (sum = sum + price);
      }, 0)
    : 0;
</script>

<table class="table table-striped mt-5 text-center">
  <thead class="table table-dark">
    <tr>
      <th>Product</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    {#each products as product}
      <tr class="list">
        <td>{product.productName}</td>
        <td>{product.price}</td>
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
