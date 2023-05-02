<script>
  import NewChar from './NewChar.svelte';
  import Info from './Info.svelte';

  export let name;

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
</script>

<main class="container">
  <div class="content">
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

<style>
  .title {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
  }

  .container {
    display: flex;
    height: 100vh;
  }

  .app {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 10vh;
  }

  .content {
    width: 80%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }

  h1 {
    font-size: 36px;
    font-weight: bold;
    margin-bottom: 20px;
    text-align: center;
  }

  button {
    display: inline-block;
    padding: 10px 20px;
    font-size: 18px;
    font-weight: bold;
    color: #fff;
    background-color: #5c867a;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #549381;
    color: rgba(255, 68, 0, 0.626);
  }

  @media (min-width: 375px) {
    main {
      max-width: none;
    }
  }
</style>
