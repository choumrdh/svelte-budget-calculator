<script>
  import{blur, slide, scale, fade, fly} from "svelte/transition";
    import { getContext } from "svelte";
  //    1st way export let expense;
  //    2nd way of doing it object destrcuting let {name, amount} = expense
  export let id;
  export let name = "";
  export let amount = 0;
  let displayAmount = false;
 
  function toggleAmount(){
      displayAmount =!displayAmount;
  }
  const removeExpense = getContext("remove")
  const setModifiedExpense = getContext("modify")
</script>

<article class="single-expense">
  <div class="expense-info">
    <h2>
      {name}
      <button class="amount-btn" on:click={toggleAmount}>
        <i class="fas fa-caret-down" />
      </button>
    </h2>
    {#if displayAmount}
      <!-- <h4 transition:blur>amount:${amount}</h4> -->
      <!-- <h4 transition:scale>amount:${amount}</h4> -->
      <!-- <h4 transition:slide>amount:${amount}</h4> -->
      <h4 in:fade out:slide>amount:${amount}</h4>
      <!-- <h4 transition:fly={{x:100, y:100, duration:2000, delay:500}}>amount:${amount}</h4> -->
    {/if}
  </div>

  <div class="expense-buttons">
    <button class="expense-btn edit-btn" on:click={()=>setModifiedExpense(id)}>
      <i class="fas fa-pen" />
    </button>
    <button class="expense-btn delete-btn" on:click={()=>removeExpense(id)}>
      <i class="fas fa-trash" />
    </button>
  </div>
</article>
