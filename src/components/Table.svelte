<script lang="ts">
  let cells: number[] = Array(10).fill(0);

  $: average = cells.reduce((x, y) => x + y) / 10
</script>

<ul>
  {#each cells as _, index}
    <li>
      <input type="number" bind:value={cells[index]} />
    </li>
  {/each}
</ul>
<p>Average: {average}</p>

<style>
</style>
