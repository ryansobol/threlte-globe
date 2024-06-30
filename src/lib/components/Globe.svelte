<script lang="ts">
	import type { MeshPhongMaterial } from 'three';

	import { Color } from 'three';
	import ThreeGlobe from 'three-globe';
	import { useThrelte } from '@threlte/core';
	import geo from '$lib/data/geo.json';

	const { scene } = useThrelte();

	const globe = new ThreeGlobe();

	scene.add(globe);

	globe
		.atmosphereAltitude(0.25)
		.atmosphereColor('#3a228a')
		.hexPolygonColor(() => 'rgba(255,255,255, 0.7)')
		.hexPolygonMargin(0.7)
		.hexPolygonResolution(3)
		.hexPolygonsData(geo.features)
		.showAtmosphere(true);

	const globeMaterial = globe.globeMaterial() as MeshPhongMaterial;

	globeMaterial.color = new Color(0x3a228a);
	globeMaterial.emissive = new Color(0x220038);
	globeMaterial.emissiveIntensity = 0.1;
	globeMaterial.shininess = 0.7;
</script>
