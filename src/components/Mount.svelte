<script>
  import { onMount } from "svelte";
  import axios from 'axios';
  
  let photos = [];
  // onMount: 컴포넌트가 DOM에 처음 렌더링 된 후에 실행
  onMount(async() => {
    const {data} = await axios.get('https://jsonplaceholder.typicode.com/photos?_limit=10');
    photos = data;
  });
</script>

<main>
  <div class="photos">
    {#each photos as photo}
      <figure>
        <img src={photo.thumbnailUrl} alt={photo.title} />
        <figcaption>{photo.title}</figcaption>
      </figure>
    {:else} 
      <p>loading...</p>
    {/each}
  </div>
</main>

<style>
  main {
    width: 1020px;
    margin: 0 auto;
  }
  .photos {
    display: grid;
    width: 100%;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 15px;
  }
  .photos img {
    width: 100%;
    vertical-align: middle;
  }
</style>