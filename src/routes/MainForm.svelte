<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import { Form, FormGroup, Button, Input, Label } from 'sveltestrap';

	const dispatch = createEventDispatcher();

	var input_postcode: any;

	async function geocode_postcode(postcode: string) {
		let call_api = async () => {
			const features: any[] = [];
			try {
				let request =
					'https://nominatim.openstreetmap.org/search?q=' +
					postcode +
					'&format=geojson&polygon_geojson=1&addressdetails=1';
				const response = await fetch(request);
				const geojson = await response.json();
				features.push(geojson);
				for (let feature of geojson.features) {
					let center = [
						feature.bbox[0] + (feature.bbox[2] - feature.bbox[0]) / 2,
						feature.bbox[1] + (feature.bbox[3] - feature.bbox[1]) / 2
					];
					let point = {
						type: 'Feature',
						geometry: {
							type: 'Point',
							coordinates: center
						},
						place_name: feature.properties.display_name,
						properties: feature.properties,
						text: feature.properties.display_name,
						place_type: ['place'],
						center: center
					};
					features.push(point);
				}
			} catch (e) {
				console.error(`Failed to forwardGeocode with error: ${e}`);
			}

			return {
				features
			};
		};

		let res = await call_api();
		return res;
	}

	function run_geocode(postcode) {
		geocode_postcode(postcode)
			.then((res) => {
				const [lon, lat] = res.features[1].center;
				dispatch('postcode', { lon, lat });
			})
			.catch((err) => {
				console.log(err);
			});
	}

	function validate() {
		console.log('Validation occured');
		geocode_postcode;
	}
</script>

<Form>
	<FormGroup>
		<Label>Enter Postcode</Label>
		<Input type="text" placeholder="Postcode" id="postcode" bind:value={input_postcode} />
	</FormGroup>
	<Button outline type="submit" on:click={run_geocode(input_postcode)}>Submit</Button>
	<Button outline type="submit">Refresh</Button>
	<Button outline type="submit">Home ward</Button>
</Form>
<Form />
