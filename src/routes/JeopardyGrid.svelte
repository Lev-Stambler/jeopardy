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
    background-color: rgb(70, 74, 197);
    width: 90vw;
    height: 90%;
  }

  .grid-item {
    font-size: 29px;
    padding: 20px;
    text-align: center;
    border: 1px rgba(148, 148, 148, 0.397) solid;
    transition: 100ms transform;
  }

  .grid-item.q:hover {
    transform: scale(1.1);
    border: 0px rgba(148, 148, 148, 0.397) solid;
    background: rgb(45, 45, 145);
  }

  .category-title {
    color: rgb(241, 241, 241);
    font-weight: 600;
  }
  
  a {
    color: rgb(235, 225, 93);
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
{#if miniGameVis}
  <MinigGame title ={currentMiniGameStr} desc = {currentDescStr} on:submit={() => { miniGameVis = false }}/>
{/if}
<div class="grid-container" in:fade>
  {#each categories as category}
    <div class="grid-item category-title">
      {category}
    </div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item q"><a href="#/question/{i}/0" class="{ visited[i][0] ? 'visited' : ''}" on:click="{() => isVisited(i, 0)}">100</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item q"><a href="#/question/{i}/1" class="{ visited[i][1] ? 'visited' : ''}" on:click="{() => isVisited(i, 1)}">200</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item q"><a href="#/question/{i}/2" class="{ visited[i][2] ? 'visited' : ''}" on:click="{() => isVisited(i, 2)}">300</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item q"><a href="#/question/{i}/3" class="{ visited[i][3] ? 'visited' : ''}" on:click="{() => isVisited(i, 3)}">400</a></div>
  {/each}
  {#each categories as category, i}
    <div class="grid-item q"><a href="#/question/{i}/4" class="{ visited[i][4] ? 'visited' : ''}" on:click="{() => isVisited(i, 4)}">500</a></div>
  {/each}
</div>

<script>
  import { fade } from 'svelte/transition';
  import MinigGame from '../general/MiniGame.svelte'
  import { getContext, setContext } from 'svelte'
  let visited = getContext('visited')
  let miniGameVis = false
  let currentMiniGameStr
  let currentDescStr
  let miniGameHit = [false, false, false]
  let numbVisited = visited.flat().reduce((red, val) => {
    console.log(val); 
    if (val === true) { return red + 1; }
    else return red; 
  }, 0)
  if (numbVisited === 7 && miniGameHit[0] === false) {
    miniGameHit[0] = true
    showMinigame('Family Feud', `People vote on decade related themes (three questions, 100 each)<br/>
What is your favorite movie of this decade?<br/>
What major US political event is the best thing to happen this decade?<br/>
If you were to vote for someone in this room to be president who would it be (can’t be your name) also no age restrictions
`)
  } else if (numbVisited === 14 && miniGameHit[1] === false) {
    miniGameHit[1] = true
    showMinigame('Charades', `Each team send one representative. If you can guess within the time limit your team wins 300 points`)
  } else if (numbVisited === 20 && miniGameHit[2] === false) {
    miniGameHit[2] = true
    showMinigame('Durak', `Two people from each team sitting diagonally (so sandwiched between two people). The team with the person in last place loses.
Ideally, don’t send children to play. Participants in charades should also not play. 300 points for the winning team.
`)
  }
  let categories = getContext('categories')
  function isVisited(i, j) {
    console.log(visited)
    visited[i][j] = true
    setContext('visited', visited)
  }
  function showMinigame(title, desc) {
    currentMiniGameStr = title
    currentDescStr = desc
    miniGameVis = true
  }
</script>