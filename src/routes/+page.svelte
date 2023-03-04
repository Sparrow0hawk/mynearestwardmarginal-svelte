<script>
	import { Styles } from 'sveltestrap';
	import Map from './Map.svelte';
	import Layout from './Layout.svelte';
</script>

<Styles />

<svelte:head>
	<title>Template maplibre-gl</title>
</svelte:head>
<Layout>
	<div slot="sidebar">
		<h1>A template svelte maplibre-gl site</h1>
	</div>

	<div slot="map">
		<Map />
	</div>
</Layout>
