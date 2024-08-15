<script>
    import { onMount } from 'svelte';
    export let params;
  
    let users = [];
    let userId = params.id; 
    let user; 
    
  
    onMount(async () => {
      const response = await fetch('data.json');
      const data = await response.json();
      users = data.users;
      user = users.find(u => u.id === userId); 
    });
  
  </script>
  
  <div>
    {#if user}
      <div class=" w-1/4 bg-slate-100 rounded-2xl p-6 m-auto flex flex-col gap-3">
        <h3>User: {user.first_name} {user.last_name}</h3>
        <!-- <p>ID: {user.id}</p> -->
        <p>Email: {user.email}</p>
        <p>Age: {user.age}</p>
        <p>Gender: {user.gender}</p>
      </div>
    {/if}
    
  </div>

