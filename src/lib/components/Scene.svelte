<script lang="ts">
	import type { MeshPhongMaterial } from 'three';

	import { Color } from 'three';
	import ThreeGlobe from 'three-globe';
	import { T, useThrelte } from '@threlte/core';
	import { OrbitControls } from '@threlte/extras';
	import polygons from '$lib/data/polygons.json';
	import flights from '$lib/data/flights.json';
	import { onMount } from 'svelte';

	const { scene } = useThrelte();

	scene.background = new Color(0x040d21);

	const globe = new ThreeGlobe();

	scene.add(globe);

	globe
		.atmosphereAltitude(0.35)
		.atmosphereColor('#3a228a')
		.hexPolygonColor(() => 'rgba(255,255,255, 0.7)')
		.hexPolygonMargin(0.7)
		.hexPolygonResolution(3)
		.hexPolygonsData(polygons)
		.showAtmosphere(true);

	const globeMaterial = globe.globeMaterial() as MeshPhongMaterial;

	globeMaterial.color = new Color(0x3a228a);
	globeMaterial.emissive = new Color(0x220038);
	globeMaterial.emissiveIntensity = 0.1;
	globeMaterial.shininess = 0.7;

	interface Flight {
		order: number;
		from: string;
		to: string;
		status: boolean;
		startLat: number;
		startLng: number;
		endLat: number;
		endLng: number;
		arcAlt: number;
	}

	onMount(() => {
		setTimeout(() => {
			globe
				.arcAltitude((f) => (f as Flight).arcAlt)
				.arcColor(() => '#D05DA6')
				.arcsData(flights)
				.arcStroke((f) => ((f as Flight).status ? 0.5 : 0.3))
				.arcDashLength(0.9)
				.arcDashGap(4)
				.arcDashAnimateTime(1000)
				.arcsTransitionDuration(1000)
				.arcDashInitialGap((f) => (f as Flight).order * 1);
		}, 2000);
	});
</script>

<T.AmbientLight args={[0xbbbbbb, 0.3]} />

<T.PerspectiveCamera makeDefault position={[0, 0, 500]}>
	<OrbitControls
		autoRotate={true}
		enableDamping={true}
		enableZoom={true}
		maxPolarAngle={Math.PI - Math.PI / 3}
		minPolarAngle={Math.PI / 3.5}
	/>

	<T.DirectionalLight args={[0xffffff, 0.8]} position={[-800, 2000, 400]} />
	<T.DirectionalLight args={[0x7982f6, 1.0]} position={[-200, 500, 200]} />

	<T.PointLight args={[0x8566cc, 10, 0, 0]} position={[-200, 500, 200]} />
</T.PerspectiveCamera>

<T.Fog args={[0x535ef3, 400, 2000]} />
