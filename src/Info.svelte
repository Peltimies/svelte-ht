<script>
  export let name;
  export let age;
  export let race;
  export let gender;
  export let stats;
  export let classi;
  import { fade, fly } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  function remove() {
    dispatch('remove', name);
  }
</script>

<div class="character-card">
  <ul>
    <li>Character name: {name}</li>
    <li>Age: {age}</li>
    <li>Race: {race}</li>
    <li>Gender: {gender}</li>

    <li>
      Str: <b style="color:red">{stats.str}</b> Mod: {Math.round(
        (stats.str - 10) / 2
      )}
    </li>
    <li>
      Dex: <b style="color:green">{stats.dex}</b> Mod: {Math.round(
        (stats.dex - 10) / 2
      )}
    </li>
    <li>
      Con: <b style="color:grey">{stats.con}</b> Mod: {Math.round(
        (stats.con - 10) / 2
      )}
    </li>
    <li>
      Int: <b style="color:purple">{stats.int}</b> Mod: {Math.round(
        (stats.int - 10) / 2
      )}
    </li>
    <li>
      Wis: <b style="color:darkblue">{stats.wis}</b> Mod: {Math.round(
        (stats.wis - 10) / 2
      )}
    </li>
    <li>
      Cha: <b style="color:hotpink">{stats.cha}</b> Mod: {Math.round(
        (stats.cha - 10) / 2
      )}
    </li>

    <li>
      Class: {classi.className.charAt(0).toUpperCase() +
        classi.className.slice(1)}
    </li>
    <li>Hit Dice: {classi.hd}</li>
    <li>Alignment: {classi.alignment}</li>
    <li>Weapons: {classi.weapons}</li>
    <li>Armor: {classi.armor}</li>
    <li>
      <p>
        Skills: {#each classi.skills as skill}
          {skill.charAt(0).toUpperCase() + skill.slice(1) + '/ '}
        {/each}
      </p>
    </li>
  </ul>
  <button on:click={remove} in:fly={{ y: 200, duration: 2000 }} out:fade
    >Delete Character</button
  >
</div>

<style>
  .character-card {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;

    align-content: center;
    width: 80%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;

    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
  }

  button {
    display: inline-block;
    padding: 10px 20px;
    font-size: 18px;
    font-weight: bold;
    color: #fff;
    background-color: #333333a0;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  /* Change the background color of the button on hover */
  button:hover {
    background-color: #666;
  }
</style>
