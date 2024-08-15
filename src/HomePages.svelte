<script>
    import { onMount } from 'svelte';
    import IdModal from './lib/IdModal.svelte';
    import AgeModal from './lib/AgeModal.svelte';
    import NameModal from './lib/NameModal.svelte';
    import EmailModal from './lib/EmailModal.svelte';
    import GenderModal from './lib/GenderModal.svelte';
    import UserList from './lib/UserList.svelte';
    import Search from './assets/img/search.png';
    import Setting from './assets/img/setting.png';
  
    let users = [];
    let originalUsers = [];
    let activeModal = null;
    let fromAge = null; 
    let toAge = null;
    let searchTerm = '';
    let showSettingsModal = false;
    let searchBy = 'all';
  
    onMount(async () => {
      const response = await fetch('data.json');
      const data = await response.json();
      users = data.users;
      originalUsers = [...data.users];
    });
    function openModal(modalType) {
      activeModal = modalType;
    }
  
    function closeModal() {
      activeModal = null;
    }
    function sortAscending() {
      users = users.slice().sort((a, b) => a.id - b.id);
    }
  
    function sortDescending() {
      users = users.slice().sort((a, b) => b.id - a.id);
    }
  
    function sortAscendingAge() {
      users = users.slice().sort((a, b) => a.age - b.age);
    }
  
    function sortDescendingAge() {
      users = users.slice().sort((a, b) => b.age - a.age);
    }
    function sortAscendingFio() {
      users = users.slice().sort((a, b) => a.first_name.localeCompare(b.first_name));
  }
  
  function sortDescendingFio() {
      users = users.slice().sort((a, b) => b.first_name.localeCompare(a.first_name));
  }
  function sortAscendingEmail() {
      users = users.slice().sort((a, b) => a.email.localeCompare(b.email));
  }
  
  function sortDescendingEmail() {
      users = users.slice().sort((a, b) => b.email.localeCompare(a.email));
  }
  function sortAscendingGender() {
      users = users.slice().sort((a, b) => a.gender.localeCompare(b.gender));
  }
  
  function sortDescendingGender() {
      users = users.slice().sort((a, b) => b.gender.localeCompare(a.gender));
  }
  async function filterAge() { 
      if (fromAge !== null && toAge !== null) {
        users = users.filter(user => user.age >= fromAge && user.age <= toAge);
        sortAscendingAge();
      } else {
        users = [...originalUsers]; 
      }
    }
    function updateFromAge(newFromAge) {
      fromAge = newFromAge;
      filterAge();
    }
  
    function updateToAge(newToAge) {
      toAge = newToAge;
      filterAge();
    }
    function handleSearch() {
      if (searchTerm.trim() === '') {
        users = [...originalUsers];
      } else {
        const searchTermLower = searchTerm.toLowerCase();
        if (searchBy === 'all') {
          users = originalUsers.filter(user => {
            return (
              user.id.toString().includes(searchTermLower) ||
              user.first_name.toLowerCase().includes(searchTermLower) ||
              user.last_name.toLowerCase().includes(searchTermLower) || 
              user.email.toLowerCase().includes(searchTermLower) ||
              user.age.toString().includes(searchTermLower)
            );
          });
        } else if (searchBy === 'name') { 
          users = originalUsers.filter(user => {
            return (
              user.first_name.toLowerCase().includes(searchTermLower) ||
              user.last_name.toLowerCase().includes(searchTermLower)
            );
          });
        } else if (searchBy.length === 2 && searchBy.includes('first_name') && searchBy.includes('last_name')) { 
          users = originalUsers.filter(user => {
            return (
              user.first_name.toLowerCase().includes(searchTermLower) ||
              user.last_name.toLowerCase().includes(searchTermLower)
            );
          });
        } else {
          users = originalUsers.filter(user => {
            return user[searchBy].toLowerCase().includes(searchTermLower);
          });
        }
      }
    }
    function setSearchBy(key) {
      searchBy = key;
    }
    
    function openSettingsModal() {
      showSettingsModal = true;
    }
  
    function closeSettingsModal() {
      showSettingsModal = false;
    }
    </script>
  
    <main>
      <div class="m-auto mt-5 w-5/6">
        <div class="m-auto bg-slate-100 mt-5 w-5/6 p-3 rounded-full flex justify-between relative">
          <div class="flex w-4/6 gap-8">
            <button on:click={handleSearch}><img class=" w-10" src={Search} alt="" /></button>
            <input class="bg-slate-100 w-5/6" placeholder="Поиск" bind:value={searchTerm} on:change={handleSearch} />
          </div> 
          <button on:click={openSettingsModal}><img class=" w-10" src={Setting} alt="" /></button>
          {#if showSettingsModal}
            <div title="Settings" class="absolute bg-slate-200 rounded-2xl  z-10  right-14">
              <div class="relative flex flex-col gap-3 p-7 ">
              <button class="absolute right-2 top-2" on:click={closeSettingsModal}>x</button>
              <button on:click={() => setSearchBy('all')}>All</button>
              <button on:click={() => setSearchBy('id')}>ID</button>
              <button on:click={() => setSearchBy(['first_name', 'last_name'])}>Name</button>
              <button on:click={() => setSearchBy('email')}>Email</button>
              <button on:click={() => setSearchBy('age')}>Age</button>
              </div>
            </div>
          {/if}
        </div>
      <div class="m-auto mt-5 w-5/6">
        <div class="bg-slate-200 p-5 rounded-t-2xl flex relative">
          <div class="w-3"></div>
          <button class="w-1/5" on:click={() => openModal('id')}>ID</button>
          <button class="w-1/5" on:click={() => openModal('name')}>Name</button>
          <button class="w-1/5" on:click={() => openModal('email')}>Email</button>
          <button class="w-1/5" on:click={() => openModal('age')}>Age</button>
          <button class="w-1/5" on:click={() => openModal('gender')}>gender</button>
          
        {#if activeModal === "id"}
          <IdModal 
          activeModal={activeModal} 
          closeModal={closeModal} 
          sortAscending={sortAscending} 
          sortDescending={sortDescending}  /> 
          {:else if activeModal === "age"}
          <AgeModal 
          activeModal={activeModal}
          closeModal={closeModal}
          sortAscending={sortAscendingAge}
          sortDescending={sortDescendingAge}
          fromAge={fromAge}
          toAge={toAge}
          filterAge={filterAge}
          updateFromAge={updateFromAge}          
          updateToAge={updateToAge}/>
          {:else if activeModal === "name"}
          <NameModal 
          activeModal={activeModal} 
          closeModal={closeModal} 
          sortAscending={sortAscendingFio} 
          sortDescending={sortDescendingFio}  />
          {:else if activeModal === "email"}
          <EmailModal 
          activeModal={activeModal} 
          closeModal={closeModal} 
          sortAscending={sortAscendingEmail} 
          sortDescending={sortDescendingEmail}  />
          {:else if activeModal === "gender"}
          <GenderModal 
          activeModal={activeModal} 
          closeModal={closeModal} 
          sortAscending={sortAscendingGender} 
          sortDescending={sortDescendingGender}  />
        {/if}
          
        </div>
  
        <UserList users={users} />
      </div>
    </main>