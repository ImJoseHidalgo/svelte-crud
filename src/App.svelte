<script>
  let products = [
    {
      id: 1,
      name: 'HP Pavilion Not',
      description: 'HP Laptop',
      category: 'laptop'
    },
    {
      id: 2,
      name: 'Razer Mouse',
      description: 'Gaming Mouse',
      category: 'peripherials'
    }
  ];
  let product = {
    id: '',
    name: '',
    description: '',
    category: '',
    imageURL: ''
  }
  const cleanProduct = () =>{
    product = {
      id: '',
      name: '',
      description: '',
      category: '',
      imageURL: ''
    }
  }

  const onSubmintHandler = e => {
    e.preventDefault();
    const newProduct = {
      id: product.length,
      name: product.name,
      description: product.description,
      category: product.category,
      imageURL: product.imageURL
    }
    products = products.concat(newProduct);
    cleanProduct();
    console.log(products)
  }
</script>

<style>
</style>

<main>
  <div class="container p-4">
    <div class="row">
      <div class="col-md-6">
        {#each products as product}
        <div class="card m-1">
          <div class="row">
            <div class="col-md-4">
              {#if !product.imageURL}
                <img src="images/no-product.jpg" alt="a" class="img-fluid p-1">
                {:else}
                <img src="{product.imageURL}" alt="a" class="img-fluid p-1">
              {/if}
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5>
                  <strong>{product.name}</strong>
                  <span>
                    <small>{product.category}</small>
                  </span>
                </h5>
                <p class="card-text">{product.description}</p>
                <button class="btn btn-danger">Delete</button>
                <button class="btn btn-secondary">Edit</button>
              </div>
            </div>
          </div>
        </div>  
        {/each}
      </div>
      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <form on:submit={onSubmintHandler}>
              <div class="form-group">
                <input class="form-control" bind:value={product.name} type="text" placeholder="Product Name" />
              </div>
              <div class="form-group">
                <textarea
                class="form-control"
                bind:value={product.description}
                id="product-description"
                rows="3"
                placeholder="Product Description" />
              </div>
              <div class="form-group">
                <input
                class="form-control"
                bind:value={product.imageURL}
                type="url"
                id="product-image-url"
                placeholder="https://imjosehidalgo.dev/" />
              </div>
              <div class="form-group">
                <select class="form-control" id="category" bind:value={product.category}>
                  <option value="laptops">Laptops</option>
                  <option value="peripherials">Peripherials</option>
                  <option value="servers">Servers</option>
                </select>
              </div>
              <button class="btn btn-secondary">Save Product</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
