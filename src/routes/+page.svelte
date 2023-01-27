<script>
    import { error } from '@sveltejs/kit';

    let inText = '';
    let inDate = '';

    function strFormat(date1, title) {
        let dateSplit = date1.split("/");
        let dateFormatted = dateSplit[2] + "-" + dateSplit[1] + "-" + dateSplit[0];
        let str = dateFormatted + "/" + title;
        console.log(str);
        return str;
    }


    // Base64 encode
    function b64EncodeUnicode(str) {
        return btoa(encodeURIComponent(str).replace(/%([0-9A-F]{2})/g, function toSolidBytes(match, p1) {
            return String.fromCharCode('0x' + p1);
        }));
    }


</script>

<svelte:head>
    <title>Advanced Countdown System - {inText}</title>
</svelte:head>

<main>
    <h1 class="title">Advanced Countdown System</h1>
    <div class="container">
        <h1>Create a countdown</h1>
        <input type="text" name="title" id="input" placeholder="Title" bind:value={inText}>
        <input type="text" name="date" id="input" placeholder="DD/MM/YYYY" bind:value={inDate}>

    <button type="submit" on:click={() => {
        let str = strFormat(inDate, inText);
        let encoded = b64EncodeUnicode(str);
        console.log(encoded);
        window.location.href = "/custom/" + encoded;
    }}>Submit</button>
    </div>
    <h4 class="copyrightText"> Copyright © COS-Soft 2022</h4>
</main>

<style>
    *{
        font-family: 'Roboto', sans-serif;
        color: rgb(255, 255, 255);
    }
    
    .container{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    input{
        width: 100%;
        padding: 12px 20px;
        margin: 8px 0;
        display: inline-block;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        background-color: rgb(240, 215, 215);
        color : rgb(0, 0, 0);
    }
    button{
        width: 100%;
        color: white;
        padding: 14px 20px;
        margin: 8px 0;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        background-color: rgba(0, 0, 0, 0.25);	
        /* Transition */
        transition: 0.5s;	
        /*animation: breathe 180s linear infinite;*/
    }
    button:hover{
        background-color: rgba(0, 0, 0, 0.5);

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
    @keyframes breathe {
 			0% {
 				background-color: rgb(78, 131, 131);
 			}
			 25% {
				background-color: rgb(212, 0, 212);
			}
			50% {
				background-color: rgb(0, 194, 194);
			}
			75% {
				background-color: rgb(235, 173, 17);
			}
			100% {
				background-color: rgb(78, 131, 131);
			}
        }
            /* title on top left */
        .title{
            position: absolute;
            top: 0;
            left: 0;
            margin: 10px;
				
}
</style>