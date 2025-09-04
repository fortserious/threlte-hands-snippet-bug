<script>
  import { T } from '@threlte/core';
  import { Controller, Hand, XR } from '@threlte/xr'

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

<Hand left >
  {#snippet wrist()}
    <T.Mesh>
      <T.IcosahedronGeometry args={[0.2]} />
      <T.MeshStandardMaterial color="turquoise" />
    </T.Mesh>
  {/snippet}
</Hand>

<Hand right>
  {#snippet wrist()}
    <T.Mesh>
      <T.IcosahedronGeometry args={[0.2]} />
      <T.MeshStandardMaterial color="hotpink" />
    </T.Mesh>
  {/snippet}
</Hand>

<Controller left />
<Controller right />