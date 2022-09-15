<script>
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'

  import Navbar from './lib/Navbar.svelte'

  import Timer from './lib/Timer.svelte'
  let timer;

  let isCounting;
  let timeInSeconds;

  window.onload = function(){

    if (Notification.permission !== "denied") {
    // We need to ask the user for permission
      Notification.requestPermission()
    }

  }

</script>

<Navbar/>
<main class="p-8 grid gap-4 justify-center text-center mt-32">
  <div>
    <button on:click={()=>{timeInSeconds=1500}}>25 Minutes</button>
    <button on:click={()=>{timeInSeconds=5}}>5 Minutes</button>
    <button on:click={()=>{timeInSeconds=900}}>15 Minutes</button>
  </div>
  
  <Timer bind:this={timer} bind:isCounting bind:timeInSeconds/>
  
  <div>
    <button on:click={()=>{isCounting=true}}>Start/Resume</button>
    <button on:click={()=>{isCounting=false}}>Stop</button>
  </div>

</main>
