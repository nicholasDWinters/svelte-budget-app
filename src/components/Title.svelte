<script lang="ts">
  import type { TypeExpense } from '../types';
  export let title = 'add expense';
  export let expenses: Array<TypeExpense> | undefined = undefined;

  let total = 0;
  $: if (expenses) {
    total = 0;
    expenses.forEach(exp => {
      total += exp?.amount;
    })
  }
</script>

<div class="main-title">
  <h2>{title}{expenses ? ` - $${total}` : ''}</h2>
</div>