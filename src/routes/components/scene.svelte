<script lang="ts">
	import { T, useTask } from '@threlte/core';
	import { interactivity, OrbitControls, Suspense } from '@threlte/extras';

	import Loading from './loading.svelte';
	import ArchLinuxLogo from './arch_linux_logo.svelte';

	interactivity();

	let rotation = $state(0);

	useTask((delta) => {
		rotation += delta;
	});
</script>

<T.PerspectiveCamera makeDefault position={[5, 5, 5]}>
	<OrbitControls maxAzimuthAngle={45} />
</T.PerspectiveCamera>

<T.DirectionalLight />
<T.AmbientLight />

<Suspense>
	{#snippet fallback()}
		<Loading />
	{/snippet}
	<ArchLinuxLogo position={[0, 0, 0]} scale={0.3} rotation.y={rotation} />
</Suspense>
