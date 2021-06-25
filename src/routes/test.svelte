<script lang="ts">
 
import { onMount } from "svelte";
let win: any;
let url;
let canvas: HTMLCanvasElement;
    onMount(()=>{
        win = window;
        console.log(win);
        canvas = document.querySelector('canvas');
        
    })
const generate = () =>{
    win.QRCode.toCanvas(canvas,url,(err) =>{
            if(err){
                alert(JSON.stringify(err))
            }
            alert("success");
        })
}
</script>
<svelte:head>
    <script defer src="js/qrcode.js"></script>
</svelte:head>

<div>
    <form on:submit|preventDefault="{generate}">
        <h3>Generate QR code </h3>
        <div class="form-group">
            <label for="url"></label>
            <input bind:value="{url}" placeholder="enter url to be converted to qrcode" class="form-control" type="text">
            <input class="btn btn-primary mt-3" type="submit" value="submit">
        </div>

    </form>
    <canvas>

    </canvas>
</div>