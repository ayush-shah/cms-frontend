<script>
  import { onMount } from "svelte";
  import { Link } from "svelte-navigator";
  let productData = [];
  onMount(async () => {
    const resProductData = await fetch(
      `http://${location.hostname}:3000/product`
    );
    productData = await resProductData.json();
  });
</script>

<div class="flex-wrapper-row">
  {#each productData as product}
    <div class="product-wrapper" id={product["_id"]}>
      <Link to={`/product/${product["_id"]}`}>
        <img
          src={product.imageLink}
          alt={product.productName}
          class="product-image"
        />
      </Link>
      <p class="product-name">
        {product.productName}
      </p>
      <!-- <p class="description">
      {product.description}
    </p> -->
      <h5 class="price">
        ₹ {product.price}
      </h5>

      <div class="addToCart">Add to cart</div>
      <!-- <h4 class="quantity">
      {product.quantity}
    </h4> -->
    </div>
  {/each}
</div>

<style scoped>
  .flex-wrapper-row {
    display: flex;
    flex-flow: row wrap;
  }

  div.product-wrapper {
    flex: 0 1 25%;
    width: 25%;
    margin: 10px;
    background: #eee;
  }

  img.product-image {
    width: 100%;
    aspect-ratio: 3/4;
    padding: 5px !important;
    object-fit: cover;
  }

  .flex-wrapper-row div > * {
    margin-bottom: 10px;
    padding: 0 5px;
  }
</style>
