<script lang="ts">
  import Title from './Title.svelte';
  import type { TypeExpense } from '../types';
import { createEventDispatcher } from 'svelte';

  let name = '';
  let amount = 0;
  let id = Math.floor(Math.random() * 1000);
  let dispatch = createEventDispatcher();
  let submitForm = () => {
    let expense: TypeExpense = { id, name, amount };
    dispatch('add', {expense: expense})
  }
</script>

<section class="form">
  <Title title="add expense" />
  <form class="expense-form">
    <div class="form-control">
      <label for="name">name</label>
      <input type="text" bind:value={name} id="name">
    </div>
    <div class="form-control">
      <label for="amount">amount</label>
      <input type="number" bind:value={amount} id="amount">
    </div>
    <p class="form-empty">
      Please fill out all form fields
    </p>
    <button type="button" class="btn btn-block" on:click={submitForm}>add expense</button>
    <button type="button" class="close-btn"><i class="fas fa-times"></i>close</button>
  </form>
</section>