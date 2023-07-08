<script>
	let categories = [];
    let data = {
        categoryId: "",
        title: "",
        url: "",
        thumbnailUrl: ""
    };
	// get data
  	async function fetchCategory(){
    	const res = await fetch('http://localhost:3000/categories');
    	categories = await res.json();
		console.log(categories);
    }
    fetchCategory();
	//POST
    async function Product() {
		await fetch('http://localhost:3000/products', {
			method: "POST",
			headers: {
          		"Content-Type": "application/json",
        	},
			body: JSON.stringify(data),
		})
	}
</script>
<button on:click={() =>{Product()}}> Click me </button> 
<input type="text" bind:value={data.title} placeholder="Title">
<input type="text" bind:value={data.url} placeholder="url">
<input type="text" bind:value={data.thumbnailUrl} placeholder="ThumbnailUrl">

<select bind:value ={data.categoryId}>
    {#each categories as category}
        <option value={category.id}>{category.title}</option>
    {/each}
</select>


