<script>
  import {onDestroy} from 'svelte';

  let seconds = 0;
  const onInterval = () => {
    const interval = setInterval(() => {
      seconds += 1;
    }, 1000);
    // onDestroy: 구성 요소가 해제 되었을 때 코드를 실행하려면
    onDestroy(() => clearInterval(interval))
  }

  onInterval();
</script>

<main>
  The page has been open for {seconds} seconds;
</main>

<style>

</style>