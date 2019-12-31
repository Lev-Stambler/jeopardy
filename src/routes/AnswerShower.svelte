<style>
  img {
    max-height: 400px;
    max-width: 100%;
    padding: 0.7rem;
  }
  .img-cont {
    display: grid;
    grid-template: "a a a a a"
                   "b b b b b"
                   "c c c c c";
    max-width: 90%;
  }
</style>
<div class="blue-container" in:fade>
  <div class="question statement">
    {@html answer}
  </div>
  <div class="img-cont">
    {#each [false, false, false, false] as item, ind}
      <!-- content here -->
      <div class="img">
        <img src="/images/{[params.category]}/{[(parseInt(params.number) + 1) * 100]}/{ind + 1}.jpg" alt="">
      </div>
      <div></div>
    {/each}
  </div>
</div>
<script>
	import { fade } from 'svelte/transition';
  export let params = {}
  import { getContext, setContext } from 'svelte'
  function goHome() {
    window.location.hash = "#/"
  }
  function correct() {
    goHome()
  }
  function wrong() {
    goHome()
  }
  let answer = getContext('answers')[params.category][params.number]
</script>