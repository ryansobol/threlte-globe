<script lang="ts">
	import { NoToneMapping } from 'three';
	import { Canvas } from '@threlte/core';
	import Scene from './Scene.svelte';
</script>

<Canvas toneMapping={NoToneMapping}>
	<Scene />
</Canvas>
