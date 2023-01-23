<svelte:head>
    <title>Semester Countdown</title>
</svelte:head>

<script>
    let remTime;
    function countdown(date){
        let now = new Date();
        let eventDate = new Date(date);
        let currentTime = now.getTime();
        let eventTime = eventDate.getTime();
        remTime = eventTime - currentTime;

        let s = Math.floor(remTime / 1000);
        let m = Math.floor(s / 60);
        let h = Math.floor(m / 60);
        let d = Math.floor(h / 24);

        h %= 24;
        m %= 60;
        s %= 60;

        h = (h < 10) ? "0" + h : h;
        m = (m < 10) ? "0" + m : m;
        s = (s < 10) ? "0" + s : s;

        return `${d} day[s], ${h} hour[s], ${m} minute[s], ${s} second[s]`;
    }
    let countdownLeft = countdown("2023-01-23");
    function counter(){
        countdownLeft = countdown("2023-01-23");
        if (remTime <= 0) {
            clearInterval(counter);
            countdownLeft = "Time's up!";
        }
    }
    setInterval(() => {
        counter();
    }, 1000);
    
</script>
<div class="countdownWrapper">
    <h1 class="countdownName">Semester Countdown</h1>
    <h1 class="countdownText">{countdownLeft}</h1>
</div>
<h4 class="copyrightText"> Copyright © COS-Soft 2022</h4>
<style>
    *{
        font-family: 'Roboto', sans-serif;
    }
    .countdownWrapper{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
    .countdownName{
      text-align: center;
      color : rgb(255, 255, 255);
    }
    .countdownText{
        text-align: center;
        color : rgb(255, 255, 255);
    }
    .copyrightText{
        color: rgb(255, 255, 255);
        font-size: 1rem;
        margin-top: 10;
        margin-bottom: 10;
        text-align: center;
        position: absolute;
        bottom: 0;  
    }
</style>