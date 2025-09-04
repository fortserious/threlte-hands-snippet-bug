<script lang="ts">
  import { Canvas, useThrelte } from '@threlte/core'
  import { VRButton } from '@threlte/xr'
  import Scene from './Scene.svelte'
  import { List, Pane, Textarea, ThemeUtils } from 'svelte-tweakpane-ui';
  import { config } from '$lib/store.svelte';
  import Scene2 from './Scene2.svelte';
  import Scene3 from './Scene3.svelte';
  import Scene4 from './Scene4.svelte';
  import { onMount } from 'svelte';
  import { Color } from 'three';
  import Frame from './Frame.svelte';

  
  let description = $derived(
    config.scene === 0 ? "Hands behind $isHandTracking if statement, child snippets for each hand." :
    config.scene === 1 ? "No $isHandTracking if statement, child snippets for each hand." :
    config.scene === 2 ? "No $isHandTracking if statement, wrist snippets for each hand." :
    "The currentWritable model is overwritten with a custom call to XRHandModelFactory"
  );

  let expectedResult = $derived(
    config.scene === 0 ? "Child snippet Icosahedron appears instead of each hand mesh (turquoise left, pink right)" :
    config.scene === 1 ? "Child snippet Icosahedron appears instead of each hand mesh (turquoise left, pink right)" : 
    config.scene === 2 ? "Hand mesh appears for each hand, with wrist snippet icosahedron on each wrist join (turquoise left, pink right)" :
    "The hand mesh appears for the left hand, and loads the onload function from the factory."
  );

  let actualResult = $derived(
    config.scene === 0 ? "Error: Uncaught ReferenceError: Cannot access 'inputSource' before initialization" : 
    config.scene === 1 ? "Bug: Icosahedrons appear at origin (since we are using reference space local-floor, at our feet) and do not move with hand" :
    config.scene === 2 ? "Bug: Icosahedrons appear at origin (since we are using reference space local-floor, at our feet) and do not move with hand" :
    "Success: the hand mesh appears for the left hand, and loads the onload function from the factory."
  )  
</script>

<Pane theme={ThemeUtils.presets.light} title="Settings">
<List bind:value={config.scene} label="Scene" options={{"Scene 1": 0, "Scene 2": 1, "Scene 3": 2, "Scene 4": 3}} />

<Textarea bind:value={description} label="Description of scene" rows={5} />
<Textarea bind:value={expectedResult} label="Expected result" rows={5} />
<Textarea bind:value={actualResult} label="Actual result" rows={5} />

</Pane>
<Canvas>

  <Frame>

  {#if config.scene === 0}

  <Scene />

  {:else if config.scene === 1}

  <Scene2 />
  
  {:else if config.scene === 2}

    <Scene3 />

  {:else}

  <Scene4 />

  {/if}

  </Frame>
</Canvas>
<VRButton />

<style>
  :global(body){
    overflow: hidden;
  }
</style>