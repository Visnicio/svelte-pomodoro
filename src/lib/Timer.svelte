<script>
    let totalSeconds = 0;
    let interval;

    let mins = 0;
    let sec = 0;

    let isCounting = true

    export function pomodoro(totalMins){
        
        totalSeconds = totalMins*60 || 0; // set the minutes in seconds format
        interval = setInterval(()=>{
            totalSeconds --;

            mins = Math.floor(totalSeconds/60);
            sec = totalSeconds % 60;

            if(!totalSeconds){
                clearInterval(interval);

                alert("End of time");
            }
        },1000)
    }

    function padTo2Digits(num) {
        return num.toString().padStart(2, '0');
    }

</script>

<div>
    <h1>{padTo2Digits(mins)} : {padTo2Digits(sec)}</h1>
</div>