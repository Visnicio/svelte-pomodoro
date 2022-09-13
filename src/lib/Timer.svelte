<script>
    let seconds = 0;
    let interval;

    let isCounting = true

    export function pomodoro(mins){
        
        seconds = mins*60 || 0; // set the minutes in seconds format
        interval = setInterval(()=>{
            seconds --;

            if(!seconds){
                clearInterval(interval);

                alert("End of time");
            }
        },1000)
    }

</script>

<div>
    <h1>{time}</h1>
</div>