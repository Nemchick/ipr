<script>
    
    export let closeModal;
    export let sortDescending;
    export let sortAscending;
  </script>

 
    <div class="absolute bg-white rounded-xl flex flex-col p-10 gap-5 left-1_5">
      <div class="relativ flex flex-col gap-5">
          <p>Sort by id</p>
        <button class=" absolute right-3 top-3" on:click={closeModal}>&#10005;</button>
        <button on:click={sortDescending}>Sort &#8593;</button>
        <button on:click={sortAscending}>Sort &#8595;</button>
      </div>
 </div>

