<script>
    
    export let timeInSeconds = 300;
    export let isCounting = false;


    let minutes;
    let seconds;

    let pomodoro;

    $: {
        seconds = Math.floor(timeInSeconds % 60);
        minutes = Math.floor(timeInSeconds/60);
    }


    pomodoro = setInterval( ()=>{
        if(isCounting){
            if(timeInSeconds > 0){
                timeInSeconds --;
            }else{
                // if (Notification.permission === "granted") {
                //     const notification = new Notification("Hi there!");
                // }
                // clearInterval(pomodoro);
            }
        }
        
    },1000)
    
    if(seconds == 0){
        console.log("acabou");
    }
    
</script>

<div class="my-10 ">
    <h1>{minutes.toString().padStart(2, '0')} : {seconds.toString().padStart(2, '0')}</h1>
</div>