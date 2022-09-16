<script>
  import { start_hydrating } from 'svelte/internal';
import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'

  import Navbar from './lib/Navbar.svelte'

  import Timer from './lib/Timer.svelte'
  let timer;

  let timeInSeconds;

  window.onload = function(){

    if (Notification.permission !== "denied") {
      // We need to ask the user for permission
      Notification.requestPermission()
    }

  }

  function addTask(){
    let task = document.querySelector("#newTask").value;
    localStorage.setItem("tasks", JSON.stringify(task)); 
  }

</script>

<Navbar/>
<main class="p-8 grid gap-4 justify-center text-center mt-32">
  <div>
    <button on:click={()=>{timeInSeconds=1500}}>25 Minutes</button>
    <button on:click={()=>{timeInSeconds=300}}>5 Minutes</button>
    <button on:click={()=>{timeInSeconds=900}}>15 Minutes</button>
  </div>
  
  <Timer bind:this={timer} bind:timeInSeconds/>
  
  <div>
    <button on:click={()=> timer.start() }>Start/Resume</button>
    <button on:click={()=> timer.stop() }>Stop</button>
  </div>

  <hr>

  <div>
    <h1>Your Tasks</h1>
    <div id="tasks">

    </div>
    <div>
      <input type="text" name="newTask" id="newTask" class="px-2 py-2 rounded-lg">
      <button on:click={()=>addTask()}>Add Task</button>
    </div>
  </div>

</main>
