<script lang="ts">
	import { Popup, Map, NavigationControl, ScaleControl } from 'maplibre-gl';
	import geojsonExtent from '@mapbox/geojson-extent';
	import { browser } from '$app/environment';
	import 'maplibre-gl/dist/maplibre-gl.css';
	import wardGeoJson from '/src/data/sheffield-wards.geojson?url';

	async function loadWards() {
		let map: Map;
		let source = 'wards';
		let layer = 'ward-layer';
		const resp = await fetch(wardGeoJson);
		const body = await resp.text();
		const json = JSON.parse(body);

		map = new Map({
			container: 'map',
			style: 'https://demotiles.maplibre.org/style.json'
		});

		let hoverId: any = null;
		function unhover() {
			if (hoverId !== null) {
				map.setFeatureState({ source: source, id: hoverId }, { hover: false });
			}
		}

		map.addControl(new ScaleControl());
		map.addControl(new NavigationControl(), 'bottom-left');

		map.on('load', function () {
			map.fitBounds(geojsonExtent(json), {
				padding: 20,
				animate: false
			});
			map.addSource(source, {
				type: 'geojson',
				data: json,
				generateId: true
			});
			map.addLayer({
				id: layer,
				source: source,
				type: 'fill',
				paint: {
					'fill-color': 'rgb(200, 100, 240)',
					'fill-outline-color': 'rgb(200, 100, 240)',
					'fill-opacity': ['case', ['boolean', ['feature-state', 'hover'], false], 0.8, 0.4]
				}
			});
			map.on('click', 'ward-layer', function (e) {
				new Popup().setLngLat(e.lngLat).setHTML(e.features[0].properties.admin_name).addTo(map);
			});
		});
	}
	loadWards();
</script>

<div id="map" />

<style>
	#map {
		position: relative;
		flex-grow: 1;
		min-height: 85vh;
	}
</style>
