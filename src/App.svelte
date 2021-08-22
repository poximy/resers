<script lang="ts">
  import Table from "./components/Table.svelte";

  let tableAverages: number[] = Array(1).fill(0);

  const createTable = () => {
    tableAverages = [...tableAverages, 0];
  };

  const deleteTable = () => {
    tableAverages.pop();
    tableAverages = tableAverages;
  };
</script>

<main>
  <table>
    <thead>
      <tr>
        <th colspan="5">weights</th>
        <th>average</th>
      </tr>
    </thead>
    <tbody>
      {#each Array(tableAverages.length) as _, index}
        <Table bind:average={tableAverages[index]} />
      {/each}
    </tbody>
  </table>
</main>

<div class="buttons">
  <button on:click={createTable}>➕</button>
  <button on:click={deleteTable}>➖</button>
</div>

<style>
</style>
