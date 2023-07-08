<script>
    import { json } from '@sveltejs/kit';

    export let data;
    let products = [];
    let categories = [];

    async function fetchProduct(categoryId) {
        let res
        if (categoryId) {
        res = await fetch('http://localhost:3000/products?categoryId');
        } 
        else {
            res = await fetch('http://localhost:3000/products');
        }
        products = await res.json();
        console.log(products);
    }
    fetchProduct();

    async function fetchCategory() {
        
        let res = await fetch('http://localhost:3000/products');
        categories = await res.json();
        console.log(categories);
    }
    fetchCategory();
 
    async function Delete(id) {
        await fetch('http://localhost:3000/products/' + '/' + id,  {
        method: "DELETE",
        headers: {
          		"Content-Type": "application/json",
        	},
            body: JSON.stringify(products),
        })
        fetchProduct();
    } 
</script>


<h1>Product list</h1>

<!-- <ul>
	{#each data.summaries as { slug, title }}
		<li><a href="/product/{slug}">{title}</a></li>
	{/each}
</ul> -->

<div>
    {#each products as product}
        <div>
            <img src="{product.thumbnailUrl}" alt="{product.title}">
            <span>{product.title}</span>
            <a href="{product.url}">View</a>
            <a href="/product/{product.id}">edit</a>
            <button on:click={() =>{Delete(product.id)}}>DELETE</button>
        </div>
    {/each}
</div>

<div>
    {#each categories as category}
        <div>
            <button on:click={() =>{fetchProduct(category.id)}}>{category.title}</button>
        </div>
    {/each}
</div>