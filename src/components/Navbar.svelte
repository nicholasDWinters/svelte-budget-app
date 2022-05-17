<script lang="ts">
  export let toggleForm: Function | undefined;
  export let showForm: boolean;
</script>

<nav class="nav">
  <div class="nav-center">
    <h1 class="nav-title">budget calculator</h1>
    {#if !showForm}
    <button class="nav-btn" type="button" on:click={() => toggleForm()}>
      <i class="far fa-plus-square" />
      add item
    </button>
    {/if}
  </div>
</nav>

<style>
  
</style>