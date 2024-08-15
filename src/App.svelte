<script>
 import Router, {location, link} from 'svelte-spa-router';
 import HomePages from './HomePages.svelte';
 import UserPage from './lib/UserPage.svelte';
</script>

<nav class=" m-auto mt-10 mb-10 w-5/6">
	<div class=" m-auto w-5/6"><a class="text-2xl bg-slate-100 p-5 text-center rounded-full " href="/">Home</a></div>
</nav> 

<Router routes={{
	'/': HomePages,
  '/user/:id': UserPage,
	
}} />