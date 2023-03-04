<script lang="ts">
	import { Form, FormGroup, Button, Input, Label } from 'sveltestrap';
</script>

<Form>
	<FormGroup>
		<Label>Enter Postcode</Label>
		<Input type="text" placeholder="Postcode" />
	</FormGroup>
	<Button outline>Submit</Button>
	<Button outline>Refresh</Button>
	<Button outline>Home ward</Button>
</Form>
