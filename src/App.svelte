<script>
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'

  import Timer from './lib/Timer.svelte'
  let timer;

  let time = 25;

  let isCounting;
</script>

<main>
  <Timer bind:this={timer} mins={time} bind:isCounting/>

  {#if isCounting===false}
    <button on:click={()=>timer.pomodoro(time)}>Start Pomodoro</button>
  {/if}
  {#if isCounting===true}
    <button on:click={()=>timer.reset(time)}>Reset</button>
  {/if}
  <button on:click={()=>{time = 25}}>25 Minutes</button>
  <button on:click={()=>{time = 5}}>5 Minutes</button>
  <button on:click={()=>{time = 15}}>15 Minutes</button>

  <h4>binding isCounting {isCounting}</h4>

</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
