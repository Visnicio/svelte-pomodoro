<script>
    let totalSeconds = 0;
    let interval;

    export let mins = 0;
    let sec = 0;

    export let isCounting = false;

    export function pomodoro(totalMins){
        isCounting = true;

        totalSeconds = totalMins*60 || 0; // set the minutes in seconds format
        
        interval = setInterval(()=>{
            totalSeconds --;

            mins = Math.floor(totalSeconds/60);
            sec = totalSeconds % 60;

            if(!totalSeconds){
                clearInterval(interval);

                alert("End of time");
                isCounting = false;
            }
        },1000)
    }

    export function pausePomodoro(){
        isCounting = false;
    }
    export function reset(){
        clearInterval(interval);
        isCounting = false;
    }

    function formatMinutes(num) {
        return num.toString().padStart(2, '0');
    }

</script>

<div>
    <h1>{formatMinutes(mins)} : {formatMinutes(sec)}</h1>
</div>