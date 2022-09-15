<script>
    
    export let timeInSeconds = 300;


    let minutes;
    let seconds;

    let pomodoro;

    $: {
        seconds = Math.floor(timeInSeconds % 60);
        minutes = Math.floor(timeInSeconds/60);
    }

    export function start(){
        pomodoro = setInterval( ()=>{
            if(timeInSeconds > 0){
                timeInSeconds --;
            }else{
                if (Notification.permission === "granted") {
                    const notification = new Notification("The time has ended");
                }
                clearInterval(pomodoro);
            }
            
        },1000)
    }

    export function stop(){
        clearInterval(pomodoro);
    }

</script>

<div class="my-10 ">
    <h1>{minutes.toString().padStart(2, '0')} : {seconds.toString().padStart(2, '0')}</h1>
</div>