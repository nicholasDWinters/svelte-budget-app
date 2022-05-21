<script lang="ts">
  import Navbar from '../components/Navbar.svelte';
  import ExpensesList from '../components/ExpensesList.svelte';
  // import expensesData from '../expenses';
  import ExpenseForm from '../components/ExpenseForm.svelte';
  import {onMount} from 'svelte';
  import type { TypeExpense } from '../types';

  onMount(() => {
    expenses = localStorage.getItem('expenses') ? JSON.parse(localStorage.getItem('expenses')) : [];
  })

  let showForm = false;
  let expenses: Array<TypeExpense> = [];
  let inProgress: TypeExpense;
 
  const setLocalStorage = () => {
    localStorage.setItem('expenses', JSON.stringify(expenses))
  }
  // dispatching events - create function in parent component (removeExpense), takes an event, contains 'details' which will hold our info that we pass through, use on:remove on the child component, use event forwarding through all other components using on:remove, and then in final child componet, Expense.svelte, create event dispatcher, and dispatch the remove event, passing through the id we need

  let removeExpense = (event: CustomEvent) => {
    expenses = expenses.filter(item => item.id !== event.detail?.id);
    setLocalStorage();
  }

  let clearExpenses = () => {
    expenses = [];
    setLocalStorage();
  }

  let addExpense = (event: CustomEvent) => {
    expenses = [event.detail?.expense, ...expenses];
    setLocalStorage();
  }
  let editExpense = (event: CustomEvent) => {
    let expense = event.detail?.expense;
    inProgress = expense;
  }

  let updateExpense = (event: CustomEvent) => {
    let expense = event.detail?.expense;
    let index = expenses.findIndex(el => el.id === expense.id);
    expenses[index] = {id: expense.id, name: expense.name, amount: expense.amount};
    inProgress = undefined;
    setLocalStorage();
  }

  let toggleForm = () => {showForm = !showForm}

</script>

<Navbar {toggleForm} {showForm} />
<main class="content">
  {#if showForm}
  <ExpenseForm on:add={addExpense} on:update={updateExpense} current={inProgress} {toggleForm} {showForm} />
  {/if}
  <ExpensesList  {toggleForm} {showForm} {expenses} on:remove={removeExpense} on:edit={editExpense} />
  <button on:click={clearExpenses} type='button' class="btn btn-primary btn-block">clear expenses</button>
</main>

<style>
  
</style>