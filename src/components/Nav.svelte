<script>
</script>

<header>
  <nav>
    <li><a href="/">1. beforeUpdate &amp; afterUpdate</a></li>
    <li><a href="mount">2. onMount</a></li>
    <li><a href="destory">3. onDestroy</a></li>
  </nav>
</header>

<style>
  header {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    background: rgba(255,255,255,0.65);
    box-shadow: 0 3px 10px rgba(0,0,0,0.15);
  }
  nav {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  nav li {
    padding: 12px 15px;
    text-transform: capitalize;
  }
  :global(nav a:hover) {
    color: rgb(0,80,160);
  }
</style>