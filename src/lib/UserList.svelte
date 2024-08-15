<script>
  export let users;
  import Href from '../assets/img/href.png';

</script>

<ul class="flex bg-slate-100 p-5 rounded-b-2xl gap-4 flex-col">
  {#each users as user}
    <li class="flex">
      <a class="w-3" data-id={user.id} href={`/user/${user.id}`}> 
        <img src={Href} alt="" />
      </a>
      <div class="w-1/5 flex justify-center"><p>{user.id}</p></div>
      <div class="w-1/5 flex justify-center"><p>{user.first_name} {user.last_name}</p></div> 
      <div class="w-1/5 flex justify-center"><p>{user.email}</p></div> 
      <div class="w-1/5 flex justify-center"><p>{user.age}</p></div>
      <div class="w-1/5 flex justify-center"><p>{user.gender}</p></div>
    </li>
  {/each}
</ul>