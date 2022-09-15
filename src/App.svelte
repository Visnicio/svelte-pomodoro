<script>
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'

  import Timer from './lib/Timer.svelte'
  let timer;

  let isCounting;
  let timeInSeconds;

</script>

<main>
  <button on:click={()=>{isCounting=true}}>Start/Resume</button>
  <button on:click={()=>{isCounting=false}}>Stop</button>

  <Timer bind:this={timer} bind:isCounting bind:timeInSeconds/>

  <button on:click={()=>{timeInSeconds=1500}}>25 Minutes</button>
  <button on:click={()=>{timeInSeconds=300}}>5 Minutes</button>
  <button on:click={()=>{timeInSeconds=900}}>15 Minutes</button>

</main>
