<script>
    import { error } from '@sveltejs/kit';
    import { page } from '$app/stores';
 
    // Base64 decode with error checking
    function b64DecodeUnicode(str) {
        try {
            return decodeURIComponent(atob(str).split('').map(function(c) {
                return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
            }).join(''));
        } catch (e) {
            error(404, e);
        }
    }
    let slug = b64DecodeUnicode($page.params.slug);
    function slugSplit(slug) {
        let slugSplit = slug.split("/");
        return slugSplit;
    }
    let splitSlug = slugSplit(slug);
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
    let countdownLeft = countdown(splitSlug[0]);
    function counter(){
        countdownLeft = countdown(splitSlug[0]);
        if (remTime <= 0) {
            clearInterval(counter);
            countdownLeft = "Time's up!";
        }
    }
    setInterval(() => {
        counter();
    }, 1000);

    console.log(slugSplit(slug));
</script>

<svelte:head>
    <title>ACS - {splitSlug[1]}</title>
    <meta name="description" content="Countdown to {splitSlug[1]}">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="theme-color" content="#ffffff">
    <link rel="icon" type="image/png" href="/favicon.png">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap">
</svelte:head>

<main>
    <div class="countdownWrapper">
        <h1 class="countdownName">{splitSlug[1]}</h1>
        <h1 class="countdownText">{countdownLeft}</h1>
    </div>
    <h4 class="copyrightText"> Copyright © COS-Soft 2022</h4>
</main>

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
