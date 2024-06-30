<script lang="ts">
	import { Color } from 'three';
	import { T, useThrelte } from '@threlte/core';
	import { OrbitControls } from '@threlte/extras';
	import Globe from './Globe.svelte';

	const { scene } = useThrelte();

	scene.background = new Color(0x040d21);
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

<Globe />
