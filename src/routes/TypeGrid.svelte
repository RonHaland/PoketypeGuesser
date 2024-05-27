<script lang="ts">
	import TypeCell from "./TypeCell.svelte";
  import data from '$lib/typeData.json';
	import type { Type } from "../types/types";
  const types = Object.keys(data) as Type[];
  const getRandomType = () => types[Math.floor(Math.random()*types.length)];
  let columns = [getRandomType(), getRandomType(), getRandomType()]
  let rows = [getRandomType(), getRandomType(), getRandomType()]
</script>

<div class="grid">
  {#each [null, ...rows] as row }
    {#each [null, ...columns] as col }
      {#if row === null && col === null}
        <span>{" "}</span>
      {/if}
      {#if row === null && col !== null}
        <span>{col}</span>
      {/if}
      {#if row !== null && col === null}
        <span>{row}</span>
      {/if}
      {#if row !== null && col !== null}
        <TypeCell attacker={row} defender={col} />
      {/if}
    {/each}
  {/each}
</div>


<style>
  .grid{
    display: grid;
    grid-template-columns: 2fr 3fr 3fr 3fr;
    grid-template-rows: 2fr 3fr 3fr 3fr;
    text-align: center;
    width: 18rem;
    height: 18rem;
  }
  span {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>