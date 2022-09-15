<script>
    export let timeInSeconds = 300;
    export let isCounting = false;

    let minutes;
    let seconds;

    let interval;

    $: {
        seconds = Math.floor(timeInSeconds % 60);
        minutes = Math.floor(timeInSeconds/60);
    }


    interval = setInterval( ()=>{
        if(isCounting){
            timeInSeconds --;
        }

    },1000)

</script>

<div>
    <h1>{minutes.toString().padStart(2, '0')} : {seconds.toString().padStart(2, '0')}</h1>
</div>