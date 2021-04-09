<script>
	export
		let
			title,			
			price,
			category,
			amount,
			image,
			id_product

	let dataOpts = [];
	let opts = [];
	let select = [];
	$: {
		dataOpts = fetch(`http://192.168.250.19:3550/opts/${id_product}`)
			.then(response => response.json())
			.then(apiResponse => {
				dataOpts = apiResponse || [];
				opts = dataOpts.opts;
				select = dataOpts.select;
			})
	}

	const handleClickBuy = () => {
		const localStorage = window.localStorage();

		localStorage.setItem('nome',title)
	}		
</script>

<!-- Modal -->
<div class="modal fade" id="modal{id_product}" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">{title}</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body pt-0">
       	<div class="container-fluid p-0">
       		<div class="row p-0">
       			<div class="col-12 p-0 img">
       				<img src="{image}" width="100%">
       			</div>
       		</div>
       		<div class="row p-0">
       			<div class="col-9 pt-2">
       				<label class="text-uppercase mb-0">{category}</label>
       			</div>
       			<div class="col-2 pt-2">
       				<b class="text-uppercase text-success text-right">${price}</b>
       			</div>
       			<div class="col-12">
       				<p class="text-justify pt-1">Deliciosos trocitos de pechuga de pollo frito y crujientes, servidas con papas fritas y Salsa de tu elección.</p>
       			</div>
       		</div>
       		{#await dataOpts}
       			<div class="row p-2">
       			{#each opts as {title, tipo, id}}
       				<div class="col-12">
	       				<div class="row bg-gray p-2 rounded">
	       					<div class="col-8 my-auto">
	       						<b class="text-gray opt">{title}</b>
	       					</div>
	       					<div class="col-4 bg-gray p-2 rounded text-center">
	       						<b class="opt text-uppercase">{tipo}</b>
	       					</div>
	       				</div>
	       			</div>
	       			{#each select as {title, price, id_opts, include}}
	       				{#if id === id_opts}
	       					{#if include === 0}
	       						<div class="col-12 mt-3 mb-3">
			       					<div class="row bg-gray p-2 rounded">
			       						<div class="col-9 text-uppercase">
			       							<b>{title}</b>
			       						</div>
			       						<div class="col-3">
			       							<b class="text-gray">
			       								{#if price <= 0}
			       								--
			       								{:else}
			       								+ ${price}
			       								{/if}
			       							</b>
			       						</div>
			       					</div>
			       				</div>
			       			{/if}
			       			{#if include === 1}
			       				<div class="col-12 mt-3 mb-3">
			       					<div class="row bg-light p-2 rounded">
			       						<div class="col-9">
			       							<b>{title}</b>
			       						</div>
			       						<div class="col-3">
			       							<b class="text-gray">
			       								{#if price <= 0}
			       								--
			       								{:else}
			       								+ ${price}
			       								{/if}
			       							</b>
			       						</div>
			       					</div>
			       				</div>
			       			{/if}	
	       				{/if}
	       			{/each}
       			{/each}
       		</div>
       		{/await}
       	</div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn border-primary text-primary" data-dismiss="modal">Cerrar</button>
        <button type="button" class="btn btn-primary" on:click={handleClickBuy}>Añadir al carrito ${price}
        </button>
      </div>
    </div>
  </div>
</div>

<style type="text/css">
	.modal-content{
		height: 97.5vh;
		overflow-y: scroll;
	}
	.img{
		height: 300px;
		overflow: hidden;
	}
	p{
		font-size: 13px;
	}
	label {
		color: rgba(0,0,0,0.5);
	}

	.und {
		font-size: 13px;
	}

	.text-gray {
		color: rgba(0,0,0,0.7);
	}

	.bg-gray{
		background: rgba(0,0,0,0.2);
	}

	.opt{
		font-size: 14px
	}
</style>