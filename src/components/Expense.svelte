<script lang="ts">
  import {createEventDispatcher} from 'svelte';
  import {slide} from 'svelte/transition';
  import type {TypeExpense} from '../types';
  export let expense: TypeExpense;
  export let showForm: boolean | undefined;
  export let toggleForm: Function | undefined;

  let displayAmount = false;

  const toggleDisplayAmount = () => displayAmount = !displayAmount;
  const dispatch = createEventDispatcher();

  const dispatchEdit = () => {
    toggleForm();
    dispatch('edit', {expense});
  }
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>{expense?.name}
      <button class:turned={displayAmount} class="amount-btn" on:click={toggleDisplayAmount}><i class="fas fa-caret-down" ></i></button>
    </h2>
    {#if displayAmount}
    <h4 transition:slide>amount: ${expense?.amount}</h4>
    {/if}
  </div>
  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={dispatchEdit}>
      <i class="fas fa-pen"></i>
    </button>
    <button on:click={() => dispatch('remove', {id: expense?.id})} class="expense-btn delete-btn">
      <i class="fas fa-trash"></i>
    </button>
  </div>
</article>

<style>
  h2 {
    margin-bottom: 0;
  }

  .turned {
    transform: rotate(180deg);
  }
</style>