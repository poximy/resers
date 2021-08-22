<script lang="ts">
  let tables: number[][] = [Array(10).fill(0)];

  const createTable = () => {
    tables = [...tables, Array(10).fill(0)];
  };

  const deleteTable = () => {
    tables.pop();
    tables = tables;
  };
</script>

<table>
  <thead>
    <tr>
      <th colspan="5">weights</th>
      <th>average</th>
    </tr>
  </thead>
  <tbody>
    {#each Array(tables.length) as _, tableNumber}
      <tr>
        {#each Array(5) as _, cellNumber}
          <td>
            <input type="number" bind:value={tables[tableNumber][cellNumber]} />
          </td>
        {/each}
        <td rowspan="2">{tables[tableNumber].reduce((x, y) => x + y) / 10}</td>
      </tr>
      <tr>
        {#each Array(5) as _, cellNumber}
          <td>
            <input
              type="number"
              bind:value={tables[tableNumber][cellNumber + 5]}
            />
          </td>
        {/each}
      </tr>
    {/each}
  </tbody>
</table>

<div class="buttons">
  <button on:click={createTable}>➕</button>
  <button on:click={deleteTable}>➖</button>
</div>

<style>
</style>
