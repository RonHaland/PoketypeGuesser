<script lang="ts">
	import TypeCell from "./TypeCell.svelte";
  import data from '$lib/typeData.json';
	import type { Type } from "../types/types";
  const types = Object.keys(data) as Type[];
  const getRandomType = () => types[Math.floor(Math.random()*types.length)];


  const getRandomTypes = (n: number) => {
    const internalTypes = [...types];
    let c = n;
    const result: Type[] = [];
    while(c){
      result.push(...internalTypes.splice(Math.floor(Math.random()*internalTypes.length),1));
      c--;
    }
    return result;
  }
  let columns = getRandomTypes(3)
  let rows = getRandomTypes(3)
  let answers = rows.map(r => columns.map(c => false));

  function updateAnswer(col: Type, row: Type, result: boolean){
    const x = rows.indexOf(row);
    const y = columns.indexOf(col);
    answers[x][y] = result;
    console.log(answers);
    console.log(row + " " + col);
    console.log(x + " " + y);
  }

  function checkAnswers() {
    const flatAnswers = answers.reduce((p, c) => [...p, ...c],[]);
    //return flatAnswers.every(f => f);
    console.log(flatAnswers);
  }
</script>

<div class="grid-container">
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
          <TypeCell attacker={row} defender={col} updateFunc={updateAnswer} />
        {/if}
      {/each}
    {/each}
  </div>
  <button on:click={checkAnswers}>Check Answers</button>
</div>

<style>
  .grid-container{
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
  }
  .grid{
    display: grid;
    grid-template-columns: 2fr 3fr 3fr 3fr;
    grid-template-rows: 2fr 3fr 3fr 3fr;
    gap: 2px;
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