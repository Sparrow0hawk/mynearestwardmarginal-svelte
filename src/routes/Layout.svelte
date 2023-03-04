<script>
	import { Col, Container, Row } from 'sveltestrap';
</script>

<Container fluid>
	<Row class="top-header">
		<Col xs="12"><slot name="title" /></Col>
	</Row>
	<Row>
		<Col xs="4"><slot name="sidebar" /></Col>
		<Col xs="8"><slot name="map" /></Col>
	</Row>
</Container>

<style>
	:global(.top-header) {
		padding-top: 2rem;
		padding-bottom: 2rem;
		background-color: rgb(230, 0, 71);
		color: white;
	}
</style>
