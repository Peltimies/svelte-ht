<script>
</script>

<div class="backdrop" />
<div class="modal">
  <header>
    <slot name="header" />
  </header>
  <slot />
  <footer>
    <slot name="footer" />
  </footer>
</div>

<style>
  .backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.75);
    z-index: 10;
  }

  .modal {
    padding: 1rem;
    position: fixed;
    top: 10vh;
    width: 50vh;
    max-height: 80vh;
    background-color: aliceblue;
    border-radius: 5px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
    overflow: auto;
  }
</style>
