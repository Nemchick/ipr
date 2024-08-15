<script>
    export let activeModal;
    export let closeModal;
    export let sortAscending; 
    export let sortDescending; 
    export let fromAge;
    export let toAge;
    export let filterAge; 
    export let updateFromAge;
    export let updateToAge;

    function resetInputs() {
    fromAge = null;
    toAge = null;
    updateFromAge(null);
    updateToAge(null);
  }
  </script>
  
  <div class="absolute bg-white rounded-xl flex flex-col p-10 left-4_5 gap-5">
    <div class="relativ flex flex-col gap-5 ">
      <p>Sort by Age</p>
      <button class="absolute right-3 top-3" on:click={closeModal}>&#10005;</button>
      <button on:click={sortDescending}>Sort &#8593;</button>
      <button on:click={sortAscending}>Sort &#8595;</button>
      <div class="flex gap-2">
        <input type="number" placeholder="from" class="border-solid border-2 rounded-xl border-slate-500 p-1 w-20" bind:value={fromAge} on:blur={() => updateFromAge(fromAge)} />
        <input type="number" placeholder="to" class="border-solid border-2 rounded-xl border-slate-500 p-1 w-20" bind:value={toAge} on:blur={() => updateToAge(toAge)} />
        
      </div>
      <div class="flex gap-10 justify-center">
        <button on:click={filterAge}>Filter</button> 
        <button on:click={resetInputs}>Reset</button> 
      </div>
    </div>
  </div>
