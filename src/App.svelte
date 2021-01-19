<script>
  import router from 'page';
  import Nav from './components/Nav.svelte';
  import Update from './components/Update.svelte';
  import Mount from './components/Mount.svelte';
  import Destory from './components/Destory.svelte';

  let page;

  router('/', () => page = Update);
  router('/mount', () => page = Mount);
  router('/destory', () => page = Destory);
  router.start();
</script>

<Nav />
<svelte:component this={page} />

<style>
	
</style>