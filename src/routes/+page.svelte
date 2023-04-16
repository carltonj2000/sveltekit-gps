<script lang="ts">
	import convert from 'geo-coordinates-parser';
	import type { PageData } from './$types';

	export let data: PageData;

	const coordinates = data.coordinates.map((c) => {
		let converted;
		try {
			converted = convert(c);
		} catch {
			console.log('convert failed for ', c);
			converted = '';
		}
		return [c, converted.decimalCoordinates];
	});
</script>

<h1>GPS Coordinate Conversion</h1>

<table>
	<thead>
		<tr>
			<th>degrees</th>
			<th>distance</th>
		</tr>
	</thead>
	<tbody>
		<tr><td>1.0</td><td>111 km</td></tr>
		<tr><td>0.1</td><td>11.1 km</td></tr>
		<tr><td>0.01</td><td>1.11 km</td></tr>
		<tr><td>0.001</td><td>111 m</td> </tr>
	</tbody>
</table>
<table>
	<thead>
		<tr>
			<th>Input</th>
			<th>Output</th>
		</tr>
	</thead>
	<tbody>
		{#each coordinates as coordinate}
			<tr>
				{#each coordinate as coordinateType}
					<td>{coordinateType}</td>
				{/each}
			</tr>
		{/each}
	</tbody>
</table>
