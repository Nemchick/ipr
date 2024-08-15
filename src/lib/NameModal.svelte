<script>
    
    export let activeModal;
    export let closeModal;
    export let sortAscending;
    export let sortDescending;
    
  </script>

  <div class="absolute bg-white rounded-xl flex flex-col p-10 gap-5 left-2_5">
    <div class="relativ flex flex-col gap-5">
        <p>Sort by Name</p>
      <button class=" absolute right-3 top-3" on:click={closeModal}>&#10005;</button>
      <button on:click={sortAscending}>A to Z</button>
      <button on:click={sortDescending}>Z to A</button>
    </div>
  </div>