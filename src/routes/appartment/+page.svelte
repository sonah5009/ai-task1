<script>
    import { PUBLIC_BASE_URL } from '$env/static/public';
 	import axios from "axios";

	let bfs_number_names = [
		{id: 261, name: `Zürich` },
		{id: 11, name: `Ottenbach` },
	];
	let rooms;
	let area;
	let price = '...'
	let selected;
	function handleSubmit() {
		let url =
            PUBLIC_BASE_URL +
            "/api/prediction/apartment?bfs_number=" +
            selected.id +
            "&area=" +
            area +
            "&rooms=" +
            rooms;
        console.log(url);
        axios.get(url).then((response) => {
            price = 'CHF ' + response.data;
        });
	}
</script>
<div class="container text-center">

	<h1>Are you paying to much? Our model predicts that you should be paying {price}</h1>

	<div class="row justify-content-md-center">
	  <div class="col col-lg-2">
		<input type="number" class="form-control" placeholder="area" aria-label="area" bind:value={area}>
	  </div>
	  <div class="col col-lg-2">
		<input type="number" class="form-control" placeholder="rooms" aria-label="rooms" bind:value={rooms}>
	  </div>
	  <div class="col col-lg-2">

		<select class="form-select" bind:value={selected}>
			{#each bfs_number_names as bfs}
				<option value={bfs}>
					{bfs.name}
				</option>
			{/each}
		</select>
	  </div>
	  <div class="col-md-auto">
		<button type="button" class="btn btn-primary" on:click={handleSubmit}>price estimation</button>
	  </div>
	</div>
  </div>