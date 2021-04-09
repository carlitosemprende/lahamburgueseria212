<script>
	import Main from './Main.svelte';
	let category = '';
	let searchInput = '';
	let search = '';
	let array = [];
	const data = (search) => {
		fetch(`http://192.168.250.19:3550/foods/${search}`)
			.then(response => response.json())
			.then(apiResponse => array = apiResponse || [])
			console.log(array);
	}
	data('');
	$: buttonHandleClick = (input) => {
		data(input);
	}

	const buttonHandleClickInput = (event) => {
		const count = event.target.value;
		if (count.length > 4) {
			category = '';
			search = event.target.value;
			console.log(search)
		} else {
			search = '';
		}
	}
</script>

<div class="container-fluid bg-white border-bottom">
	<div class="row">
		<div class="col-12">
			<div class="container">
				<div class="row pb-2">
					<div class="col-3 p-2">
						<img src="https://i.imgur.com/18zcYn9.png" class="mx-auto">
					</div>
					<div class="col-9 my-auto pr-0">
						<div class="dropdown show">
						  <a class="btn btn-white border form-control dropdown-toggle" href="#" role="button" id="dropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
						    Categorias
						  </a>

						  <div class="dropdown-menu" aria-labelledby="dropdownMenuLink">
						    <a class="dropdown-item" href="#" on:click={() => buttonHandleClick('')}>Todos</a>
						    <a class="dropdown-item" href="#" on:click={() => buttonHandleClick('entradas')}>Entradas</a>
						    <a class="dropdown-item" href="#" on:click={() => buttonHandleClick('hamburguesas')}>Hamburguesas</a>
						    <a class="dropdown-item" href="#" on:click={() => buttonHandleClick('postres')}>Postres</a>
						    <a class="dropdown-item" href="#" on:click={() => buttonHandleClick('bebidas')}>Bebidas</a>
						  </div>
						</div>
					</div>
					<div class="col-12 col-md-5 mt-2 my-auto border rounded pr-0">
						<div class="row  pr-0">
							<div class="col-1 my-auto">
								<i class="fa fa-search"></i>
							</div>
							<div class="col-10 pr-0 mr-0">
								<input type="text" class="form-control bg-white mr-0" placeholder="Buscar comida" value={searchInput}  on:input={buttonHandleClickInput}/>
							</div>
						</div>
					</div>
				</div>	
			</div>
		</div>
	</div>
</div>

<Main data={array} />

<style type="text/css">

	img {
		width: 100%;
	}

	input{
		border: none;
	}


	i{
		font-size: 20px;
	}
</style>