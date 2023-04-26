<script>
  import Modali from './Modali.svelte';

  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let result;

  async function rollDice() {
    try {
      const response = await fetch('https://rolz.org/api/?3d6.json');
      const data = await response.json();
      result = data;
      rolledResult = result.result;
      console.log(result.result);
      return rolledResult;
    } catch (error) {
      console.error(error);
    }
  }

  async function allStats() {
    str = await rollDice();
    dex = await rollDice();
    con = await rollDice();
    int = await rollDice();
    wis = await rollDice();
    cha = await rollDice();
    rolledStats = {
      str: str,
      dex: dex,
      con: con,
      int: int,
      wis: wis,
      cha: cha,
    };
  }

  $: str = 0;
  $: dex = 0;
  $: con = 0;
  $: int = 0;
  $: wis = 0;
  $: cha = 0;

  $: rolledResult = 0;

  let genders = ['Male', 'Female'];
  let races = ['Human', 'Elf', 'Anturai'];
  let classes = [
    {
      className: 'assassin',
      primAtr: 'dex',
      hd: '1d6',
      alignment: 'any non-good',
      weapons: 'any',
      armor: 'light',
      skills: [
        'case target',
        'climb',
        'death attack',
        'disguise',
        'hide',
        'listen',
        'move silently',
        'poisons',
        'sneak attack',
        'traps',
      ],
    },
    {
      className: 'barbarian',
      primAtr: 'con',
      hd: '1d12',
      alignment: 'any',
      weapons: 'any',
      armor: 'any',
      skills: [
        'combat sense',
        'deerstalker',
        'intimidate',
        'primeval instincts',
        'whirlwind attack',
        'primeval will',
        'ancestral calling',
      ],
    },
    {
      className: 'bard',
      primAtr: 'cha',
      hd: '1d10',
      alignment: 'any',
      weapons: ['simple'],
      armor: 'light',
      skills: [
        'decipher script',
        'exalt',
        'legend lore',
        'fascinate',
        'exhort',
        'greatness',
      ],
    },

    {
      className: 'cleric',
      primAtr: 'wis',
      hd: '1d8',
      alignment: 'any',
      weapons: 'blunt',
      armor: 'any',
      skills: ['chosen spells', 'turn undead'],
    },

    {
      className: 'druid',
      primAtr: 'wis',
      hd: '1d8',
      alignment: 'neutral (any)',
      weapons: 'simple',
      armor: 'light',
      skills: [
        'bonus language',
        'nature lore',
        'resist elements',
        'woodland stride',
        'totem shape',
        'spells',
      ],
    },

    {
      className: 'fighter',
      primAtr: 'str',
      alignment: 'any',
      hd: '1d10',
      weapons: 'any',
      armor: 'any',
      skills: ['weapon specialization', 'combat dominance', 'extra attack'],
    },

    {
      className: 'illusionist',
      primAtr: 'int',
      alignment: 'any',
      hd: '1d4',
      weapons: 'simple',
      armor: 'none',
      skills: ['disguise', 'spell casting', 'sharp senses'],
    },

    {
      className: 'knight',
      primAtr: 'cha',
      alignment: 'any',
      weapons: 'any except code-of-conduct limitations',
      armor: 'any',
      skills: [
        'birthright mount',
        'horsemanship',
        'inspire',
        'embolden',
        'demoralize',
        'call to arms',
      ],
    },

    {
      className: 'monk',
      primAtr: 'con',
      alignment: 'any lawful',
      weapons: 'simple',
      armor: 'none',
      skills: [
        'fast movement',
        'hand-to-hand combat',
        'iron body',
        'stun attack',
        'deflect missiles',
        'iron fists',
        'slow fall',
        'feign death',
        'fast healing',
        'iron mind',
        'death strike',
      ],
    },

    {
      className: 'paladin',
      primAtr: 'cha',
      alignment: 'lawful good',
      hd: '1d10',
      weapons: 'any',
      armor: 'any',
      skills: [
        'cure disease',
        'detect evil',
        'divine aura',
        'divine health',
        'lay on hands',
        'turn undead',
        'divine mount',
        'aura of courage',
        'smite evil',
        'divine healing',
      ],
    },

    {
      className: 'ranger',
      primAtr: 'str',
      alignment: 'any',
      hd: '1d10',
      weapons: 'any',
      armor: 'medium',
      skills: [
        'combat marauder',
        'conceal',
        'delay/neutralize poison',
        'favored enemy',
        'move silently',
        'scale',
        'traps',
        'survival',
        'track',
      ],
    },

    {
      className: 'rogue',
      primAtr: 'dex',
      alignment: 'any',
      hd: '1d6',
      weapons: 'simple & martial',
      armor: 'light',
      skills: [
        'back attack',
        'cant',
        'climb',
        'decipher script',
        'hide',
        'listen',
        'move silently',
        'open lock',
        'pick pockets',
        'traps',
        'sneak attack',
      ],
    },

    {
      className: 'wizard',
      primAtr: 'int',
      alignment: 'any',
      hd: '1d4',
      weapons: 'simple',
      armor: 'none',
      skills: 'spell casting',
    },

    {
      className: 'plague doctor',
      primAtr: 'int',
      alignment: 'any',
      hd: '1d6',
      weapons: 'simple',
      armor: 'light',
      skills: [
        'plague knowledge',
        'identify substance',
        'alchemy',
        'healing touch',
        'poison resistance',
        'plague mask',
      ],
    },

    {
      className: 'warlock',
      primAtr: 'cha',
      alignment: 'any neutral or evil',
      hd: '1d6',
      armor: 'light',
      weapons: 'simple',
      skills: [
        'pact magic',
        'dark ones blessing',
        'otherworldy patron',
        'devils tongue',
      ],
    },
  ];

  let chosenName = '';
  let chosenAge = '';
  let chosenGender = genders[0];
  let chosenClass = classes[0];
  let chosenRace;
  let rolledStats = {};

  const save = () =>
    dispatch('save', {
      chosenName: chosenName,
      chosenAge: chosenAge,
      chosenGender: chosenGender,
      chosenClass: chosenClass,
      chosenRace: chosenRace,
      rolledStats: rolledStats,
    });
  const close = () => dispatch('close');

  let warning = '*Please give your character a name';
  let ageWarning = '*Please give your character an age above 18';

  $: nameValid = chosenName.length > 0;
  $: ageValid = chosenAge >= 18;

  let nameVisited = false;
  let ageVisited = false;

  $: console.log(
    chosenName,
    chosenAge,
    chosenGender,
    chosenRace,
    chosenClass.className,
    chosenClass.hd,
    chosenClass.alignment,
    chosenClass.weapons,
    chosenClass.armor,
    chosenClass.skills
  );
</script>

<Modali>
  <h2>Roll your character</h2>
  <button class="close-btn" on:click={close} name="close"
    ><img class="imits" src="./pics/svgcross.svg" alt="Exit cross" /></button
  >
  <div class="modal-content">
    <div class="inputs">
      <div>
        <label for="name">Name</label>
        <input
          on:blur={() => {
            nameVisited = true;
          }}
          type="text"
          bind:value={chosenName}
        />

        {#if nameVisited && !nameValid}
          <p id="varoitus" style="color: red;">{warning}</p>
        {/if}
      </div>
      <div>
        <label for="age">Age</label>
        <input
          on:blur={() => {
            ageVisited = true;
          }}
          type="number"
          bind:value={chosenAge}
        />

        {#if ageVisited && !ageValid}
          <p id="varoitus" style="color: red;">{ageWarning}</p>
        {/if}
      </div>

      <select id="races" bind:value={chosenRace}>
        {#each races as race}
          <option value={race}>{race}</option>
        {/each}
      </select>
      <div>
        {#each genders as gender}
          <label>
            <input
              type="radio"
              name="gender"
              value={gender}
              bind:group={chosenGender}
            />
            {gender}
          </label>
        {/each}
      </div>
    </div>
    <div class="footer">
      <div class="footer-content">
        <button class="die" on:click={allStats}
          ><img class="d20" src="./pics/twenty-sided-dice.svg" alt="d20" />
        </button>

        <div class="choice">
          {#if str}
            <p>Str is {str}</p>
            <p>Dex is {dex}</p>
            <p>Con is {con}</p>
            <p>Int is {int}</p>
            <p>Wis is {wis}</p>
            <p>Cha is {cha}</p>
          {:else}
            <p>Str is {str}</p>
            <p>Dex is {dex}</p>
            <p>Con is {con}</p>
            <p>Int is {int}</p>
            <p>Wis is {wis}</p>
            <p>Cha is {cha}</p>
          {/if}

          <select bind:value={chosenClass}>
            {#each classes as classi}
              <option value={classi}
                >{classi.className.charAt(0).toUpperCase() +
                  classi.className.slice(1)}</option
              >
            {/each}
          </select>
        </div>

        <div>
          <button
            class="save"
            disabled={!nameValid || !ageValid || !str}
            on:click={save}
            name="save">Save Character</button
          >
        </div>
      </div>
    </div>
  </div></Modali
>

<style>
  .choice {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    align-items: center;
    align-content: stretch;
  }
  .modal-content {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: stretch;
    align-content: stretch;
  }

  .inputs {
    display: flex;
    gap: 20px;
  }

  .footer-content {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
  }
  input {
    border: none;
    border-bottom: 1px solid black;
    background-color: transparent;
    font-weight: bold;
    color: red;
  }

  .save {
    margin-top: 2rem;
  }
  .close-btn {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    background-color: transparent;
  }

  .imits {
    width: 20px;
    height: 20px;
  }

  .d20 {
    width: 50px;
    height: 50px;
  }

  .d20:hover {
    transition: 0.3;
    color: #549381;
  }

  .die {
    border: none;
    background-color: transparent;
    color: #666;
    text-align: center;
  }

  .die:hover {
    transition: 0.3;
    color: #549381;
  }

  .save:disabled {
    background-color: #666;
  }

  .save {
    display: inline-block;
    padding: 10px 20px;
    font-size: 18px;
    font-weight: bold;
    color: #fff;
    background-color: #782222;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  input[type='radio'] {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    border: 2px solid #ddd;
    border-radius: 50%;
    width: 20px;
    height: 20px;
    outline: none;
    transition: all 0.2s ease-in-out;
  }

  input[type='radio']:checked {
    border-color: #782222;
    background-color: #782222;
  }

  input[type='radio']:focus {
    box-shadow: 0 0 2px 2px red;
  }

  select {
    appearance: none;
    padding: 0.5rem 2rem 0.5rem 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 1rem;
    font-family: Arial, sans-serif;
    color: red;
    font-weight: bold;

    background-color: transparent;

    background-position: right 0.7rem center;
  }
</style>
