<script>
  async function getProductDetails() {
    const resproductDetails = await fetch(
      `http://${location.hostname}:3000/product/${id}`
    );
    return await resproductDetails.json();
  }
  export let id;
</script>

{#await getProductDetails()}
  Loading...
{:then product}
  <div class="product-wrapper" id={product["_id"]}>
    <img
      src={product.imageLink}
      alt={product.productName}
      class="product-image"
    />
    <div class="detail-flex-wrapper">
      <div class="detail-wrapper">
        <p class="title">Product Name</p>
        <p class="product-name">
          {product.productName}
        </p>
      </div>
      <div class="detail-wrapper">
        <p class="title">Description</p>
        <p class="description">
          {product.description}
        </p>
      </div>
      <div class="detail-wrapper">
        <p class="title">Price:</p>
        <h5 class="price">
          ₹ {product.price}
        </h5>
      </div>
      <div class="detail-wrapper">
        <p class="title">Stock Left:</p>
        <h5 class="quantity">
          {product.quantity}
        </h5>
      </div>
      <div class="addToCart">Add to cart</div>
    </div>
  </div>
{:catch error}
  {error}
{/await}}

<style>
  img.product-image {
    width: 40%;
    margin: 10%;
    aspect-ratio: 3/4;
    object-fit: cover;
  }

  .product-wrapper {
    display: flex;
    flex-flow: row wrap;
  }
  .detail-flex-wrapper {
    display: flex;
    flex-flow: column wrap;
    align-self: center;
  }

  p.title {
    font-weight: bold;
    margin: 5px 0;
  }

  .detail-wrapper {
    margin: 10px 0;
  }
  .addToCart {
    margin: 5% 0;
    width: 100%;
  }
</style>
