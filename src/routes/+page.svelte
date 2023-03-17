<script>
	import { Styles } from 'sveltestrap';
	import Map from './Map.svelte';
	import Layout from './Layout.svelte';
	import MainForm from './MainForm.svelte';

	let lon;
	let lat;

	function handlePostcode(e) {
		lon = e.detail.lon;
		lat = e.detail.lat;
	}
</script>

<Styles />

<svelte:head>
	<title>mynearestsheffieldmarginal</title>
</svelte:head>
<Layout>
	<div slot="title">
		<h1>mynearestsheffieldmarginal</h1>
	</div>

	<div slot="sidebar">
		<h2>Another subtitle</h2>
		<MainForm on:postcode={handlePostcode} />
	</div>

	<div slot="map">
		<Map {lon} {lat} />
	</div>
</Layout>
