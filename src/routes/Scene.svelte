<script>
  import { T } from '@threlte/core';
  import { XR, Controller, Hand, useXR } from '@threlte/xr'

  const { isHandTracking } = useXR()

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

{#if $isHandTracking}

<Hand left >
      <T.Mesh>
    <T.IcosahedronGeometry args={[0.2]} />
    <T.MeshStandardMaterial color="turquoise" />
  </T.Mesh>
</Hand>

<Hand right>
      <T.Mesh>
    <T.IcosahedronGeometry args={[0.2]} />
    <T.MeshStandardMaterial color="pink" />
  </T.Mesh>
</Hand>

{:else}

<Controller left />
<Controller right />
{/if}

