<script lang="ts">
	import type { MeshPhongMaterial } from 'three';

	import { Color } from 'three';
	import ThreeGlobe from 'three-globe';
	import { T, useThrelte } from '@threlte/core';
	import { OrbitControls } from '@threlte/extras';
	import geo from '$lib/data/geo.json';

	const { scene } = useThrelte();

	scene.background = new Color(0x040d21);

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

	<T.PointLight args={[0x8566cc, 0.5]} position={[-200, 500, 200]} />
</T.PerspectiveCamera>

<T.Fog args={[0x535ef3, 400, 2000]} />
