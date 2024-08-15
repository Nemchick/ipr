<script>
 import Router, {location, link} from 'svelte-spa-router';
 import HomePages from './HomePages.svelte';
 import UserPage from './lib/UserPage.svelte';
</script>

<nav>
	<a  href="/">Home</a>
</nav> 

<Router routes={{
	'/': HomePages,
  '/user/:id': UserPage,
	
}} />