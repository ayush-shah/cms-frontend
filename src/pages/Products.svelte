<script>
  async function categories() {
    const categories = await fetch("http://localhost:3000/product/category");
    return categories.json().then((result) => {
      return [...new Set(result)];
    });
  }
  let productName, category, price, quantity, description, imageLink;
  async function submitFormData() {
    var myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");

    var raw = JSON.stringify({
      productName: productName.value,
      category: category.value,
      price: price.value,
      quantity: quantity.value,
      description: description.value,
      imageLink: imageLink.value,
    });

    var requestOptions = {
      method: "POST",
      headers: myHeaders,
      body: raw,
      redirect: "follow",
    };

    fetch("http://localhost:3000/product/insert", requestOptions)
      .then((response) => response.text())
      .then((result) => console.log(result))
      .catch((error) => console.log("error", error));
  }
</script>

<form
  on:submit|preventDefault={submitFormData}
  class="insert-product"
  autocomplete="off"
>
  <label for="productName">Product Name</label>
  <input
    type="text"
    name="productName"
    placeholder="Product Name"
    required
    bind:this={productName}
  />
  <label for="category">Category</label>
  <input
    list="category"
    placeholder="Select Category"
    name="category"
    bind:this={category}
  />
  <datalist id="category">
    {#await categories()}
      Loading...
    {:then category}
      {#each category as category}
        <option value={category}>{category}</option>
      {/each}
    {/await}
  </datalist>
  <label for="price">Price</label>
  <input
    type="number"
    name="price"
    step="0.01"
    placeholder="Price"
    required
    bind:this={price}
  />
  <label for="quatity">Quantity</label>
  <input
    type="number"
    name="quantity"
    placeholder="Quantity"
    required
    bind:this={quantity}
  />
  <label for="description">Description</label>
  <textarea
    placeholder="Description Here.."
    name="description"
    required
    bind:this={description}
  />
  <label for="imageLink">Upload Images</label>
  <input
    type="text"
    placeholder="Enter URL"
    name="imageLink"
    bind:this={imageLink}
  />
  <input type="submit" value="Submit" />
</form>

<style scoped>
  form.insert-product {
    width: 50%;
    min-height: 50%;
    margin: auto;
    position: relative;
    display: flex;
    padding: 15px;
    flex-flow: column;
  }

  form.insert-product > * {
    flex: 1 0;
    border: none;
    /* box-shadow: 1px 1px 4px #5555; */
    margin: 10px 0;
  }

  form.insert-product input,
  form.insert-product textarea {
    box-shadow: 1px 4px 4px #0005;
    padding: 8px 15px;
    outline: none;
  }
</style>
