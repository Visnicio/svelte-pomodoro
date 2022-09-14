<script>
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'

  import Timer from './lib/Timer.svelte'
  let timer;

  let isCounting;
  let mins;
</script>

<main>
  <Timer bind:this={timer} bind:mins bind:isCounting/>

  {#if isCounting===false}
    <button on:click={()=>timer.startPomodoro(mins)}>Start Pomodoro</button>
  {/if}
  {#if isCounting===true}
    <button on:click={()=>timer.pausePomodoro(mins)}>Pause</button>
  {/if}
  {#if isCounting===true}
    <button on:click={()=>timer.pausePomodoro()}>Resume</button>
  {/if}
  <button on:click={()=>{mins = 25}}>25 Minutes</button>
  <button on:click={()=>{mins = 5}}>5 Minutes</button>
  <button on:click={()=>{mins = 15}}>15 Minutes</button>

  <h4>binding isCounting {isCounting}</h4>
  <h4>binding mins {mins}</h4>

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
