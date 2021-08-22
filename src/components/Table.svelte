<script lang="ts">
  export let average: number;

  let cells: number[] = Array(10).fill(0);
  $: average = cells.reduce((x, y) => x + y) / 10;
</script>

<tr>
  {#each Array(5) as _, index}
    <td>
      <input type="number" bind:value={cells[index]} />
    </td>
  {/each}
  <td>{average}</td>
</tr>
<tr>
  {#each Array(5) as _, index}
    <td>
      <input type="number" bind:value={cells[index + 5]} />
    </td>
  {/each}
</tr>

<style>
</style>
