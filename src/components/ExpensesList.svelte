<script lang="ts">
  import type { TypeExpense } from '../types';
  import Expense from './Expense.svelte'
  import Title from './Title.svelte';
  export let expenses: Array<TypeExpense>;
  export let toggleForm: Function | undefined;
  export let showForm: boolean | undefined;
</script>

<section>
  <Title title="expense list" {expenses} />
  <ul>
    {#each expenses as expense, index}
    <Expense {toggleForm} {showForm}  {expense} on:remove on:edit />
    {:else}
    <h2>currently no expenses to show</h2>
    {/each}
  </ul>
</section>

<style>
  h2 {
    text-transform: capitalize;
    color: red;
  }
</style>