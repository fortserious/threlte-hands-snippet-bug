<script>
  import { Canvas } from '@threlte/core'
  import { VRButton, XR } from '@threlte/xr'
  import Scene from './Scene.svelte'
  import { List, Pane, Textarea, ThemeUtils } from 'svelte-tweakpane-ui';
  import { config } from '$lib/store.svelte';
  import Scene2 from './Scene2.svelte';
  import Scene3 from './Scene3.svelte';

  let description = $derived(
    config.scene === 0 ? "Hands behind $isHandTracking if statement, child snippets for each hand." :
    config.scene === 1 ? "No $isHandTracking if statement, child snippets for each hand." :
    "No $isHandTracking if statement, wrist snippets for each hand."
  );

  let expectedResult = $derived(
    config.scene === 0 ? "Child snippet Icosahedron appears instead of each hand mesh (turquoise left, pink right)" :
    config.scene === 1 ? "Child snippet Icosahedron appears instead of each hand mesh (turquoise left, pink right)" : 
    "Hand mesh appears for each hand, with wrist snippet icosahedron on each wrist join (turquoise left, pink right)"
  );

  let actualResult = $derived(
    config.scene === 0 ? "Uncaught ReferenceError: Cannot access 'inputSource' before initialization" : 
    config.scene === 1 ? "Icosahedrons appear at origin (since we are using reference space local-floor, at our feet)" :
    "Icosahedrons appear at origin (since we are using reference space local-floor, at our feet)" 
  )
</script>

<Pane theme={ThemeUtils.presets.light} title="Settings">
<List bind:value={config.scene} label="Scene" options={{"Scene 1": 0, "Scene 2": 1, "Scene 3": 2}} />

<Textarea bind:value={description} label="Description of scene" rows={5} />
<Textarea bind:value={expectedResult} label="Expected result" rows={5} />
<Textarea bind:value={actualResult} label="Actual result" rows={5} />
</Pane>
<Canvas>

  {#if config.scene === 0}

  <Scene />

  {:else if config.scene === 1}

  <Scene2 />

  {:else}

  <Scene3 />

  {/if}
</Canvas>
<VRButton />

<style>
  :global(body){
    overflow: hidden;
  }
</style>