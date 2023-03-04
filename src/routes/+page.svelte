<script>
	import { Styles } from 'sveltestrap';
	import Map from './Map.svelte';
	import Layout from './Layout.svelte';
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
	</div>

	<div slot="map">
		<Map />
	</div>
</Layout>
