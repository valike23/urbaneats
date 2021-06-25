<script lang="ts">
import { onMount } from "svelte";

let win: any;
let video: HTMLVideoElement;
let scanner: any;

onMount(()=>{
    win = window;
    console.log(win);
    video = document.querySelector('video');
    
   
  
    
})

const submit = () => {
    scanner = new win.Instascan.Scanner({video: video});
    win.Instascan.Camera.getCameras().then(function (cameras) {
	if (cameras.length > 0) {
	  scanner.start(cameras[0]);
	} else {
	  console.error('No cameras found.');
	}
  }).catch(function (e) {
	console.error(e);
  });

  scanner.addListener('scan', function (content) {
	alert(content);
    scanner.stop();
  });
}
</script>
<svelte:head>
    <script defer src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script defer src="https://rawgit.com/schmich/instascan-builds/master/instascan.min.js"></script>
</svelte:head>

<div class="container">
   <!-- svelte-ignore a11y-media-has-caption -->
   <video></video>
   <button on:click="{submit}" class="btn btn-primary">Start Scan</button>
   
</div>