<script>
  import darkMode from './darkMode.js';

  let modalStyle = '';

  $: modalStyle = `
  background-color: ${$darkMode ? '#333' : 'var(--bg-color'};
    color: ${$darkMode ? '#fff' : '#333'};
    transition: 1s;
  `;
</script>

<div class="backdrop" />
<div class="modal" style={modalStyle}>
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
    width: 80%;
    max-height: 80vh;

    border-radius: 5px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.25);
    overflow: scroll;
  }
</style>
