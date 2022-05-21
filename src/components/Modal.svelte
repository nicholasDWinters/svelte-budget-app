<script lang="ts">
import {fade, fly} from 'svelte/transition';
</script>

<div class="modal-container" transition:fade>
  <div class="modal-content" transition:fly={{y:200}}>
    <slot />
  </div>
</div>