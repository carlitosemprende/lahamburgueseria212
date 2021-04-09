<script>
	import Article from './components/Article.svelte';		
	export 
		let 
			data	

</script>

<main class="container-fluid bg-white">
	<section class="row border-bottom">
			{#each data as {title,price,category,amount,image,id}}
				<Article
				title={title}
				price={price}
				category={category}
				amount={amount}
				image={image}
				id={id}
				/>
			{:else}
				<strong>No hay productos</strong>	
			{/each}	
	</section>
</main>

