<script lang="ts">
  import Title from './Title.svelte';
  import type { TypeExpense } from '../types';
import { createEventDispatcher } from 'svelte';
  export let toggleForm: Function | undefined;
  export let current: TypeExpense;
  let name = '';
  let amount = 0;
  let id = Math.floor(Math.random() * 1000);
  let addForm = true;
  $: error = name.length === 0;
  $: addForm;

$: if (current && addForm) {
   addForm = false;
   name = current.name;
   amount = current.amount;
   id = current.id;
 }
  
 let resetValues = () => {
    name = '';
    amount = 0;
    id = Math.floor(Math.random() * 1000);
 }

  let dispatch = createEventDispatcher();
  let submitForm = () => {
    
      let expense: TypeExpense = { id, name, amount };
      if (addForm) {
        dispatch('add', {expense});
        resetValues();
        toggleForm();
      } else {
        dispatch('update', {expense});
        resetValues();
        addForm = true;
        toggleForm();
      }
    
  }

  let closeForm = () => {
    resetValues();
    addForm = true;
    toggleForm();
  }

</script>


<section class="form">
  <Title title={addForm ? 'add expense' : 'edit expense'} />
  <form class="expense-form">
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" bind:value={name} id="name">
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" min="0" bind:value={amount} id="amount">
    </div>
    {#if error}
    <p class="form-empty">
      Please fill out all form fields
    </p>
    {/if}
    <button type="button" class:disabled={error} disabled={error} class="btn btn-block" on:click={submitForm}>{addForm ? 'add expense' : 'edit expense'}</button>
    <button on:click={closeForm} type="button" class="close-btn"><i class="fas fa-times"></i>close</button>
  </form>
</section>
