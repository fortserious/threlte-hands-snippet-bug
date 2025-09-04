<script>
  import { useThrelte } from "@threlte/core";
  import { onMount } from "svelte";
  import { Color } from "three";
  
  let { children } = $props();

  let {scene, invalidate } = useThrelte();

      onMount(()=>{
    setBG()
})
  export function setBG()
  {        
    scene.background = new Color(0xffffff);
    invalidate()
  }
</script>

{@render children()}