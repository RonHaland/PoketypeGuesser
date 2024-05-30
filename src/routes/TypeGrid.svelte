<script lang="ts">
	import TypeCell from "./TypeCell.svelte";
  import data from '$lib/typeData.json';
	import type { Type } from "../types/types";
  const types = Object.keys(data) as Type[];

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
  let answers = rows.map(() => columns.map(() => false));
  let resultOpen = false;
  let results = {correct: 0, total: 9};

  function updateAnswer(col: Type, row: Type, result: boolean){
    const x = rows.indexOf(row);
    const y = columns.indexOf(col);
    answers[x][y] = result;
    resultOpen = false;
  }

  function checkAnswers() {
    const flatAnswers = answers.reduce((p, c) => [...p, ...c],[]);
    results = {correct: flatAnswers.filter(f => f).length, total: flatAnswers.length};
    resultOpen = true;
  }

  function reroll() {
    columns = getRandomTypes(3);
    rows = getRandomTypes(3);

    answers = rows.map(() => columns.map(() => false));
    resultOpen = false;
  }
</script>

<div class="grid-container">
  <div class="grid">
    {#each [null, ...rows] as row (row) }
      {#each [null, ...columns] as col (col)}
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
  <div class={`results ${resultOpen ? '' : 'hidden'}`}>
    <span>{results.correct} out of {results.total} are correct</span>
  </div>
  <button on:click={reroll}>Reroll</button>
</div>

<style>
  .grid-container{
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
  .grid{
    display: grid;
    grid-template-columns: 2fr 3fr 3fr 3fr;
    grid-template-rows: 2fr 3fr 3fr 3fr;
    gap: .5rem;
    text-align: center;
    width: 18rem;
    height: 18rem;
  }
  .results{
    font-size: 1.5rem;
    margin: 0 2rem;
    height: 2rem;
  }
  .hidden>span{
    display: none;
  }
  button{
    padding: 0.5rem;
    border-radius: .75rem;
    border: 1px solid black;
    margin: 0.5rem 2rem;
    background: rgb(49, 70, 59);
    color:aliceblue;
    transition: scale 0.1s ease-in-out;
  }
  button:hover{
    scale:1.1;
  }
  button:hover::after{
    border-radius: .5rem;
    content:' ';
    display: block;
    inset:0;
    position: absolute;
    pointer-events: none;
    background: rgba(255, 255, 255, 0.18);
  }
  span {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>