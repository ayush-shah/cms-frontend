<script>
  let deleteSuccess = false;
  async function getProductDetails() {
    const resproductDetails = await fetch(
      `http://${location.hostname}:3000/product/id=${id}`
    );
    return await resproductDetails.json();
  }
  async function deletePrompt(id) {
    if (confirm("Do you want me to delete?")) {
      const deleteConfirmation = await fetch(
        `http://${location.hostname}:3000/product/delete/${id}`,
        { method: "delete" }
      );
      if (deleteConfirmation.status === 200) {
        deleteConfirmation.json().then(async () => {
          deleteSuccess = true;
          let timeout = await setTimeout(() => {
            deleteSuccess = false;
          }, 2000);
        });
      } else {
        alert("Something went wrong");
      }
    }
  }
  export let id;
</script>

{#await getProductDetails()}
  Loading...
{:then product}
  <div class="product-wrapper" id={product["_id"]}>
    {#if deleteSuccess}
      <div class="delete-success" bind:this={deleteSuccess}>
        Deleted Successfully
      </div>
    {/if}
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
      <div
        class="removeProduct"
        on:click={() => {
          deletePrompt(product["_id"]);
        }}
      >
        <i class="gg-trash" />
      </div>
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
    flex: 0 1;
  }

  .product-wrapper {
    display: flex;
    flex-flow: row wrap;
    position: relative;
    padding: 0 5vw;
  }
  .detail-flex-wrapper {
    flex: 1 0;
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
    width: 50%;
  }
  .delete-success {
    opacity: 0;
    background: #7ace7a;
    padding: 15px 5vw;
    position: absolute;
    color: #fff;
    width: 100%;
    left: 0;
    top: 0;
    animation: show 2s linear both;
  }
  @keyframes show {
    from {
      opacity: 0;
    }
    15% {
      opacity: 1;
    }
    85% {
      opacity: 1;
    }
    to {
      opacity: 0;
    }
  }
  .gg-trash {
    box-sizing: border-box;
    position: relative;
    display: block;
    transform: scale(var(--ggs, 1));
    width: 10px;
    height: 12px;
    border: 2px solid transparent;
    box-shadow: 0 0 0 2px, inset -2px 0 0, inset 2px 0 0;
    border-bottom-left-radius: 1px;
    border-bottom-right-radius: 1px;
    margin-top: 4px;
  }

  .gg-trash::after,
  .gg-trash::before {
    content: "";
    display: block;
    box-sizing: border-box;
    position: absolute;
  }

  .gg-trash::after {
    background: currentColor;
    border-radius: 3px;
    width: 16px;
    height: 2px;
    top: -4px;
    left: -5px;
  }

  .gg-trash::before {
    width: 10px;
    height: 4px;
    border: 2px solid;
    border-bottom: transparent;
    border-top-left-radius: 2px;
    border-top-right-radius: 2px;
    top: -7px;
    left: -2px;
  }
</style>
