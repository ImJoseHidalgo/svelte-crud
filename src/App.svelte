<script>
  import {v4} from 'uuid';
  import Noty from 'noty';
  import 'noty/lib/noty.css';
  import 'noty/lib/themes/sunset.css'

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
  let editStatus = false;
  const cleanProduct = () =>{
    product = {
      id: '',
      name: '',
      description: '',
      category: '',
      imageURL: ''
    }
  }

  const addProduct = () => {
    const newProduct = {
      id: v4(),
      name: product.name,
      description: product.description,
      category: product.category,
      imageURL: product.imageURL
    }
    products = products.concat(newProduct);
    cleanProduct();
    console.log(products)
  };

  const updateProduct = () => {
    let updatedProduct = {
      name: product.name,
      description: product.description,
      id: product.id,
      imageURL: product.imageURL,
      category: product.category
    }
    const productIndex = products.findIndex(p => p.id == product.id)
    products[productIndex] = updatedProduct;
    cleanProduct();
    editStatus = false;
    new Noty ({
      theme: 'sunset',
      type: 'success',
      timeout: 3000,
      text: 'Card Actualizado Padre'
    }).show();
  }
  const onSubmintHandler = e => {
    if(!editStatus) {
      addProduct();
    } else {
      updateProduct();
    }
  };

  const deleteProduct = (id) => {
    products = products.filter(product => product.id != id);
  }
  const editProduct = productEdited => {
    product = productEdited;
    editStatus = true;
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
                <button
                  class="btn btn-danger"
                  on:click={deleteProduct(product.id)}>
                  Delete</button>
                <button
                  class="btn btn-secondary"
                  on:click={editProduct(product)}>
                  Edit</button>
              </div>
            </div>
          </div>
        </div>  
        {/each}
      </div>
      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <form on:submit|preventDefault={onSubmintHandler}>
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
              <button class="btn btn-secondary">
                {#if !editStatus}
                  Save Product
                  {:else}
                    Update Product
                {/if}
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>
