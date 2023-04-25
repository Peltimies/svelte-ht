<script>
  import NewChar from './NewChar.svelte';
  import Info from './Info.svelte';
  import darkMode from './darkmode.js';
  export let name;

  function toggleDarkMode() {
    darkMode.update((value) => !value);
  }

  //ce.detaili ottaa vastaan välitetyn datan äitikomponentilla muualla välitetyn custom eventin avulla
  function removeWithId(ce) {
    characters = characters.filter(
      (character) => character.chosenName != ce.detail
    );
    characters = characters;
  }

  let showModal = false;

  let characters = [];

  function addChar(ce) {
    characters.push(ce.detail);
    characters = characters;
    showModal = false;
  }
  $: console.log(characters);

  let darken = '';

  $: darken = `
    background-color: ${$darkMode ? '#333' : 'var(--bg-color'};
    color: ${$darkMode ? '#fff' : '#333'};
    transition: 1s;
  `;
</script>

<!--ternary joka vaihtelee tumman ja vaalean teeman väliltä koko body elementtiä-->
<body style={darken}>
  <main class="container">
    <div class="content">
      <button on:click={toggleDarkMode}>
        {#if $darkMode}
          Turn off dark mode
        {:else}
          Turn on dark mode
        {/if}
      </button>
      <div class="title">
        <h1>Character Generator</h1>
        <p>Harjoitustyö by <b>{name}</b></p>
      </div>
      <div class="app">
        <button class="glow-on-hover" on:click={() => (showModal = true)}
          >Roll a Character</button
        >

        {#if showModal}
          <NewChar on:save={addChar} on:close={() => (showModal = false)} />
        {/if}
      </div>
      <div class="character info">
        {#each characters as character}
          <Info
            on:remove={removeWithId}
            name={character.chosenName}
            age={character.chosenAge}
            race={character.chosenRace}
            gender={character.chosenGender}
            stats={character.rolledStats}
            classi={character.chosenClass}
            hitDie={character.hd}
            alignment={character.alignment}
            weapons={character.weapons}
            armor={character.armor}
            skills={character.skills}
          />{/each}
      </div>
    </div>
  </main>
  <footer />
</body>

<style>
  .title {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }
  body {
    height: auto;
    width: auto;
  }
  .container {
    display: flex;
  }

  /* Center the app on the page */
  .app {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 10vh;
  }

  /* Set the width of the main content area */
  .content {
    width: 80%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }

  /* Style the heading */
  h1 {
    font-size: 36px;
    font-weight: bold;
    margin-bottom: 20px;
    text-align: center;
  }

  /* Style the button */
  button {
    display: inline-block;
    padding: 10px 20px;
    font-size: 18px;
    font-weight: bold;
    color: #fff;
    background-color: var(--primary-color);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  /* Change the background color of the button on hover */
  button:hover {
    background-color: #549381;
    color: rgba(255, 68, 0, 0.626);
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
