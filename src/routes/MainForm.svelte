<script lang="ts">
	import { Form, FormGroup, Button, Input, Label } from 'sveltestrap';

	function validate() {
		console.log('Validation occured');
	}
</script>

<Form on:submit={validate}>
	<FormGroup>
		<Label>Enter Postcode</Label>
		<Input type="text" placeholder="Postcode" />
	</FormGroup>
	<Button outline type="submit">Submit</Button>
	<Button outline>Refresh</Button>
	<Button outline>Home ward</Button>
</Form>
