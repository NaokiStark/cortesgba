<script>
	// @ts-nocheck

	import 'leaflet/dist/leaflet.css';

	import { LeafletMap, TileLayer, Marker, DivIcon } from 'svelte-leafletjs';

	const mapOptions = {
		center: [-34.6291088, -58.4554624],
		zoom: 10
	};

	const tileUrl = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png';
	const tileLayerOptions = {
		minZoom: 0,
		maxZoom: 20,
		maxNativeZoom: 19,
		attribution: '© OpenStreetMap contributors'
	};

	const iconOptMedia = {
		html: '<div class="map-icon media"> </div>'
	};
	const iconOptBaja = {
		html: '<div class="map-icon baja"> </div>'
	};

	let leafletMap;
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<main>
	<!--	-->
	<div class="referencias">
		{#if contents}
			{@html contents}
		{/if}
		<div>
			<h4 style="margin:2px">Referencias</h4>
			<span style="display: inline-block" class="map-icon media" />
			Cortes media tensión
			<br />
			<span style="display: inline-block" class="map-icon baja" />
			Cortes baja tensión
		</div>
	</div>
	{#if addressPoints_Cuadro_D}
		<LeafletMap bind:this={leafletMap} options={mapOptions}>
			<TileLayer url={tileUrl} options={tileLayerOptions} />
			{#each addressPoints_Cuadro_D as point}
				{#if point[2] == 11 || point[2] == 12}
					<Marker latLng={[point[0], point[1]]}>
						<DivIcon options={iconOptMedia} />
					</Marker>
				{/if}
				{#if point[2] == 21 || point[2] == 22}
					<Marker latLng={[point[0], point[1]]}>
						<DivIcon options={iconOptBaja} />
					</Marker>
				{/if}
			{/each}
		</LeafletMap>
	{/if}
</main>

<style>
	:global(body, html, main) {
		height: 100%;
		padding: 0;
		margin: 0;
		overflow: hidden;
	}
	main {
		display: block;
	}
	:global(.leaflet-container) {
		position: initial !important;
	}

	:global(.leaflet-div-icon) {
		background: none;
		border: none;
	}

	:global(.map-icon) {
		width: 10px;
		height: 10px;
		border-radius: 25px;
		background-color: white;
		border: solid 1px #333;
	}

	:global(.map-icon.media) {
		width: 12px;
		height: 12px;
		background-color: rgb(194, 58, 58);
	}

	:global(.map-icon.baja) {
		width: 7px;
		height: 7px;
		background-color: rgb(58, 101, 194);
	}

	.referencias {
		position: absolute;
		z-index: 9999;
		border-radius: 5px;
		background-color: #fff;
		padding: 1em;
		font-family: Arial, Helvetica, sans-serif;
	}

	:global(h1, h3, p) {
		margin: 2px;
	}
	:global(h1) {
		font-size: 1.3em;
	}
	:global(h2) {
		font-size: 1.1em;
	}
	:global(h3) {
		font-size: 1em;
	}
</style>
