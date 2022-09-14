<script>
    let totalSeconds;
    let interval;

    export let mins = 0;
    let sec = 0;

    export let isCounting = false;

    export function pomodoro(totalMins){
        
        totalSeconds = totalMins*60 || 0; // set the minutes in seconds format
        
        isCounting = true;

        // interval = setInterval(()=>{

        //     if(isCounting){
        //         totalSeconds --;

        //         mins = Math.floor(totalSeconds/60);
        //         sec = totalSeconds % 60;

        //         if(!totalSeconds){
        //             clearInterval(interval);

        //             isCounting = false;

        //             let sound = new Audio("../assets/sounds/clock.mp3");
        //             sound.play();
        //         }
        //     }
        // },1000)
    }

    export function pausePomodoro(){
        isCounting = false;
    }
    export function reset(){
        clearInterval(interval);
        
        isCounting = false;
    }

    export function startPomodoro(totalMins){
        totalSeconds = totalMins*60 || 0; // set the minutes in seconds format
        
        isCounting = true;
    }

    function formatMinutes(num) {
        return num.toString().padStart(2, '0');
    }

    interval = setInterval(()=>{

        if(isCounting){
            totalSeconds --;
    
            mins = Math.floor(totalSeconds/60);
            sec = totalSeconds % 60;
    
            if(!totalSeconds){
                clearInterval(interval);
    
                isCounting = false;
    
                let sound = new Audio("../assets/sounds/clock.mp3");
                sound.play();
            }
        }
    },1000)

</script>

<div>
    <h1>{formatMinutes(mins)} : {formatMinutes(sec)}</h1>
</div>