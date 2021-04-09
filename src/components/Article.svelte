<script>	
	import ArticleModal from './ArticleModal.svelte';	
	export
		let
			title,			
			price,
			category,
			amount,
			image,
			id
</script>

<article class="col-10 mx-auto border-bottom mb-2 mt-4">
	<div class="row">
		<div class="col-5 bg-light mb-4 rounded text-light img p-0">
			<img src="{image}" width="100%" class="p-0">
		</div>
		<div class="col-6 mx-auto pr-0 my-auto">
			<div class="row">
				<div class="col-12 mx-auto mb-1 rounded p-0">
					<div class="row p-0">
						<div class="col-8">
							<p class="mb-0 pb-0 text-uppercase">{title}</p>
						</div>
						<div class="col-4 my-auto">
							<b class="und">{amount} UND</b>
						</div>
					</div>
				</div>
				<div class="col-8 mr-auto mb-2 rounded p-0">
					<label class="mb-0 text-uppercase">{category}</label>
				</div>
				<div class="col-4 ml-auto mb-2 rounded p-0 text-right">
					<b class="text-success">${price}</b>
				</div>
				<div class="col-12 mx-auto mb-4 p-0">
					<button class="form-control btn border" data-toggle="modal" data-target="#modal{id}"><i class="fa fa-shopping-cart"></i></button>
				</div>
			</div>	
		</div>
	</div>
</article>

<ArticleModal
	title={title}
	price={price}
	category={category}
	amount={amount}
	image={image}
	id_product={id}
/>

<style type="text/css">
	.img{
		height: 124px;
		overflow: hidden;
	}

	.img img{
		width: 100%;
	}

	label {
		font-size: 13px;
		color: rgba(0,0,0,0.5);
	}

	p{
		font-size: 14px;
	}

	.und {
		font-size: 12px;
	}
</style>
