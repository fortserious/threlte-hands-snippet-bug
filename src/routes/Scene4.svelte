<script lang="ts">
  import { T, useThrelte } from '@threlte/core';
  import { Controller, Hand, useHand, XR } from '@threlte/xr'
  import { MeshBasicMaterial, SkinnedMesh } from 'three';
  import { XRHandModelFactory } from 'three/examples/jsm/Addons.js';

  const factory = new XRHandModelFactory(null, turnRed);

  const { renderer} = useThrelte();
  const{ xr } = renderer;
  const hand = useHand('left')
  const model = factory.createHandModel(xr.getHand(0), 'mesh');
  const store = $derived(hand);

export async function turnRed()
{
    if (model?.children?.[0]?.children?.[0])
    {
        console.log("turning hand red");
        (model.children[0].children[0] as SkinnedMesh).material = new MeshBasicMaterial({color: 0xff0000});
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

<Hand left>
{#if $store?.hand}
<T is={$store.hand}>    
    <T is={model} />           
  </T>
{/if}
</Hand>

<Hand right />

<Controller left />
<Controller right />