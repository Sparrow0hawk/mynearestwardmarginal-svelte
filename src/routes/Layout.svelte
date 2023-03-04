<script>
	import { Col, Container, Row } from 'sveltestrap';
</script>

<Container fluid>
	<Row>
		<Col xs="4"><slot name="sidebar" /></Col>
		<Col xs="8"><slot name="map" /></Col>
	</Row>
</Container>
