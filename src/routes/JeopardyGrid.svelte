<style>
  .grid-container {
    display: grid;
    /* grid-template-columns: 20% 20% 20% 20% 20%; */
    grid-template: "a a a a a"
                   "b b b b b"
                   "c c c c c";
  }
  .grid-container {
    display: inline-grid;
    background-color: #060CE9;
  }

  .grid-item {
    font-size: 29px;
    padding: 20px;
    text-align: center;
    border: 1px black solid;
  }

  .category-title {
    color: rgb(241, 241, 241);
    font-weight: 600;
  }
  
  a {
    color: rgb(253, 240, 48);
    text-decoration: none;
  }

  a:hover {
    text-decoration: underline;
  }

  a.visited:hover {
    cursor: not-allowed;
    text-decoration: none!important;
  }

  a.visited {
    /* color: rgb(145, 141, 97); */
    color: rgb(145, 141, 97);
  }

</style>
<div class="grid-container">
  {#each categories as category}
    <div class="grid-item category-title">
      {category}
    </div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item"><a href="#/question/{i}/0" class="{ visited[i][0] ? 'visited' : ''}" on:click="{() => isVisited(i, 0)}">100</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item"><a href="#/question/{i}/1" class="{ visited[i][1] ? 'visited' : ''}" on:click="{() => isVisited(i, 1)}">200</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item"><a href="#/question/{i}/2" class="{ visited[i][2] ? 'visited' : ''}" on:click="{() => isVisited(i, 2)}">300</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item"><a href="#/question/{i}/3" class="{ visited[i][3] ? 'visited' : ''}" on:click="{() => isVisited(i, 3)}">400</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item"><a href="#/question/{i}/4" class="{ visited[i][4] ? 'visited' : ''}" on:click="{() => isVisited(i, 4)}">500</a></div>
  {/each}
</div>

<script>
  import { getContext, setContext } from 'svelte'
  let visited = getContext('visited')

  export let categories = ["fake", "fake", "fake", "fake", "fake"]
  function isVisited(i, j) {
    console.log(visited)
    visited[i][j] = true
    setContext('visited', visited)
  }
</script>