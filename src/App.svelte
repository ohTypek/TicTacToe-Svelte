<script lang="ts">
  import Fields from "./lib/fields.svelte";

  const signs:string[] = ['X', 'O'];

  let turn:number = 1;
  let wins = { x: 0, o: 0 }

  function randomEmoji() {
    const emojis:string[] = [
      '🎉','🥳','🎊','🏆','🥂','👏','🍾','✨','🔥'
    ];

    const index:number = Math.floor(Math.random() * emojis.length);
    return emojis[index];
  }
  
</script>

<main>
  <nav>
    <h2>
      O - Wygrane: {wins.o}
    </h2>
    <h2> │ </h2>
    <h2>
      X - Wygrane: {wins.x}
    </h2>
  </nav>
  <div id="center">
    
  {#if wins.x > 4 || wins.o > 4}
  <h1>
    <p class="emoji">{randomEmoji()}{randomEmoji()}</p>
    {signs[(turn-1)%2]} wygrał grę
    <p class="emoji">{randomEmoji()}{randomEmoji()}</p>
  </h1>
  {:else}
  <h3>Tura: {signs[turn%2]}</h3>
  <div id="board">
    <Fields bind:turn={turn} bind:current_sign={signs[turn%2]} bind:wins={wins}/>
  </div>
  {/if}
  </div>
</main>

<style>
  nav {
    position: relative;
    width: 100%;
    display: flex;
    gap: 100px;
    justify-content: center;
    background-color: var(--board-color);
  }

  nav h2 {
    font-size: 32px;
  }

  #center {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -200px;
    margin-left: -150px;
  }

  #board {
    display: grid;
    grid-template-columns: repeat(3, var(--field-size));
    gap: 10px;
    background-color: var(--board-color);
    width: fit-content;
  }

  h1 {
    background-color: var(--board-color);
    padding: 5px 60px;
    border-radius: 5px;
    text-align: center;
    grid-column: span 3;
  }

  .emoji {
    grid-column: span 3;
    text-align: center;
  }
</style>
