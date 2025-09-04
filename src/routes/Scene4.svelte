<script lang="ts">
  import { T } from '@threlte/core';
  import { Controller, Hand, useHand, XR } from '@threlte/xr'
  import { onMount, tick } from 'svelte';
  import { Material, MeshBasicMaterial, SkinnedMesh } from 'three';

const hand = useHand('left')

  const store = $derived(hand);
 const model = $derived($store?.model);

$inspect("model", model);

export async function turnRed()
{
    await tick();

    console.log(model);
        if (model?.children?.[0]?.children?.[0])
{
    console.log("turning hand red");
    (model.children[0].children[0] as SkinnedMesh).material = new MeshBasicMaterial({color: 0xff0000});
}
else
{
    console.log("no skinnedmesh found", $state.snapshot(model));
}
}

</script>
<T.PerspectiveCamera
  makeDefault
  position={[10, 10, 10]}
  oncreate={(ref) => {
    ref.lookAt(0, 1, 0)
  }}
/>

<T.DirectionalLight position={[0, 10, 10]} />

<XR />

<Hand left onconnected={turnRed}>
{#if $store?.hand}
<T is={$store.hand}>    
    <T is={model} />           
  </T>
{/if}
</Hand>

<Hand right>

</Hand>

<Controller left />
<Controller right />