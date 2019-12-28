<script>
	import { onMount } from 'svelte';
  onMount(() => {
    var clock = new FlipClock(jQueryStuff('.your-clock'), 33, {
    // ... your options here
    clockFace: 'MinuteCounter',
    autoPlay: true,
    countdown: true,
    });
  })
</script>
<div class="container">
<div class="your-clock"></div>
</div>

<style>
  .container {
    transform: scale(0.7);
    padding: 20px;
    border-radius: 10px;
  }
</style>