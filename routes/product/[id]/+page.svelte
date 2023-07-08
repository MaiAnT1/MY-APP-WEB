<script>
	export let data;
	let product = {};
	let categories =[];
	let EditProduct = {
        categoryId: "",
        title: "",
        url: "",
        thumbnailUrl: ""
    };
	async function fetchdata() {
		let res = await fetch('http://localhost:3000/products/' + data.id);
		EditProduct = await res.json();
		console.log(EditProduct);
	};
	fetchdata();

	async function edit() {
		await fetch('http://localhost:3000/products/' + data.id , {
			method: "PUT",
			headers: {
          		"Content-Type": "application/json",
        	},
			body: JSON.stringify(EditProduct),
		});
	}

	async function fetchCategory(){
    	const res = await fetch('http://localhost:3000/categories');
    	categories = await res.json();
		console.log(categories);
    }
	fetchCategory();
</script>

{JSON.stringify(data)}

<h1>{data.id}</h1>
 
<button on:click={() =>{edit()}}> EDIT </button>
<input type="text" bind:value={EditProduct.title} placeholder="Title" >
<input type="text" bind:value={EditProduct.url} placeholder="url" >
<input type="text" bind:value={EditProduct.thumbnailUrl} placeholder="thumbnailUrl" >

<select bind:value ={EditProduct.categoryId}>
    {#each categories as category}
        <option value={category.id}>{category.title}</option>
    {/each}
</select>
