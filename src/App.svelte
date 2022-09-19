<script>

  // Import the functions you need from the SDKs you need
  import { initializeApp } from "@firebase/app";
  import { getAnalytics } from "@firebase/analytics";
  // TODO Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries
  import { getFirestore, collection, addDoc, setDoc, getDoc, doc, updateDoc, arrayUnion, query, where, onSnapshot } from "@firebase/firestore";
  import { getAuth, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "@firebase/auth";

 

  // Your web app's Firebase configuration
  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "AIzaSyAfFN6Anifz0ZzfnhypQjT7DBHrWJbqUnc",
    authDomain: "pumadoro-d01cd.firebaseapp.com",
    projectId: "pumadoro-d01cd",
    storageBucket: "pumadoro-d01cd.appspot.com",
    messagingSenderId: "780330437681",
    appId: "1:780330437681:web:3729b08a8100e9034d1910",
    measurementId: "G-KY8ZJMH7FZ"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);
  const db = getFirestore(app);
  const auth = getAuth();

  import Navbar from './lib/Navbar.svelte'
  import Task from './lib/Task.svelte'
  import Timer from './lib/Timer.svelte'

  let timer;
  let userTasks = [];
  let timeInSeconds;
  let userLogged = false;

  let unsubscribe;

  window.onload = function(){

    if (Notification.permission !== "denied") {
      Notification.requestPermission()
    }

  }

  function signIn(){
    const provider = new GoogleAuthProvider();

    signInWithPopup(auth, provider)
    .then((result) => {
      // This gives you a Google Access Token. You can use it to access the Google API.
      const credential = GoogleAuthProvider.credentialFromResult(result);
      const token = credential.accessToken;
      // The signed-in user info.
      const user = result.user;

    }).catch((error) => {
      const errorCode = error.code;
      const errorMessage = error.message;
      const email = error.customData.email;
      const credential = GoogleAuthProvider.credentialFromError(error);
    });
  }

  onAuthStateChanged(auth, user =>{
    if(user){

      const q = query(collection(db, "tasks"), where("userId", "==", user.uid)); //make a query to select all documents of this user
      unsubscribe = onSnapshot(q, (querySnapshot) => {
        const tasks = [];
        querySnapshot.forEach( (doc) => {
          tasks.push(doc.data());
        })
        userTasks = tasks;
      })

      userLogged = true;
    }else{

      userLogged = false;

      unsubscribe();
    }
  })

  async function addTask(){
    let task = document.querySelector("#newTask").value;

    const user = auth.currentUser;

    if (user !== null){
      const ref = collection(db, "tasks");
      await addDoc(ref, {
        task: task,
        userId: user.uid,
        finished: false
      })
    }

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
    {#if userLogged == true}
      <div id="signedIn">
        <div>
          <input type="text" name="newTask" id="newTask" class="px-2 py-2 rounded-lg">
          <button on:click={()=>addTask()}>Add Task</button>
          <button on:click={()=>signOut(auth).then(()=>{})}>Sign out</button>
        </div>
        <div id="tasks">
          {#each userTasks as task}
            <Task task={task.task} isFinished={task.finished}/>
          {/each}
        </div>
      </div>
    {:else if userLogged == false}
      <div id="signedOut">
        <h2 class="mt-10">Sign in with google to get your tasks</h2>
        <button class="mt-5" on:click={()=>signIn()}>Sign In</button>
      </div>
    {/if}
  </div>

</main>
