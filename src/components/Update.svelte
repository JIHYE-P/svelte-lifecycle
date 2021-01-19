<script>
  import Eliza from 'elizabot';
  import {afterUpdate, beforeUpdate} from 'svelte';
  const eliza = new Eliza();

  let div;
  let autoscroll;
  let comments = [
    {author: 'eliza', text: eliza.getInitial()}
  ]
  
  // beforeUpdate(callback: () => void) 상태 변경 후 구성요소가 업데이트 되기 직전에 실행됨
  beforeUpdate(() => {
    autoscroll = div && (div.offsetHeight + div.scrollTop) > (div.scrollHeight - 20);
  });

  // afterUpdate(callback: () => void) 구성 요소가 업데이트 된 후 즉시 실행됨
  afterUpdate(() => {
    if(autoscroll) div.scrollTo(0, div.scrollHeight);
  });

  const handleKeydown = (ev) => {
    if(ev.keyCode === 13){
      const text = ev.target.value;
      if(!text) return;
      comments = comments.concat({
        author: 'user',
        text
      });
      ev.target.value = '';

      const reply = eliza.transform(text);
      setTimeout(() => {
        comments = comments.concat({
          author: 'eliza',
          text: '...',
          placeholder: true
        });
        
        setTimeout(() => {
          comments = comments.filter(comment => !comment.placeholder).concat({
            author: 'eliza',
            text: reply
          })
        }, 500 + Math.random() * 500)
      }, 200 + Math.random() * 200)
    }
  }
</script>

<h1 style="text-transform: capitalize">1. beforeUpdate &amp; afterUpdate</h1>
<main>
  <!-- bind:this={div} 엘리먼트 반환 -->
  <h1>Chat Eliza</h1>
	<div class="scrollable" bind:this={div}>
    {#each comments as comment}
      <article class={comment.author}>
        <span>{comment.text}</span>
      </article>
    {/each}
  </div>
  <input on:keydown={handleKeydown} />
</main>

<style>
	main {
    display: flex;
    flex-direction: column;
    height: 75%;
    padding: 30px 20px;
    max-width: 320px;
    margin: 0 auto;
    background: #f8f8f8;
    border-radius: 1em;
    box-shadow: 0 8px 15px rgba(0,0,0,0.15);
  }
  h1 {
    margin-bottom: 15px;
    text-align: center;
    font-size: 22px;
  }
	.scrollable {
		flex: 1 1 auto;
		border-top: 1px solid #eee;
		margin: 0 0 1.1em 0;
    overflow-y: auto;
    
    padding: 15px;
	}

	article {
    margin: 0.5em 0;
    font-size: 13px;
	}

	.user {
		text-align: right;
	}

	span {
		padding: 0.5em 1em;
		display: inline-block;
	}

	.eliza span {
		background-color: #eee;
		border-radius: 1em 1em 1em 0;
	}

	.user span {
		background-color: #0074D9;
		color: white;
		border-radius: 1em 1em 0 1em;
  }
  
  input {
    padding: 0.5em 1em;
    font-size: 13px;
    border: 1px solid #eee;
    border-radius: 5px;
    background: #fff;
  }
  input:focus {
    border-color: #333;
  }
</style>