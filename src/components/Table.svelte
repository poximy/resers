<script lang="ts">
  let tables: number[][] = [Array(10).fill(0)];

  const calcTableAverage = (cellValues: number[]) => {
    const total = cellValues.reduce((x, y) => x + y);
    return total / 10;
  };

  const createTable = () => {
    tables = [...tables, Array(10).fill(0)];
  };

  const deleteTable = () => {
    tables.pop();
    tables = tables;
  };
</script>

<div class="main-table">
  <table>
    <thead>
      <tr>
        <th colspan="5">weights</th>
        <th>average</th>
      </tr>
    </thead>
    <tbody>
      {#each Array(tables.length) as _, tableNumber}
        <tr class="top">
          {#each Array(5) as _, cellNumber}
            <td>
              <input
                type="number"
                bind:value={tables[tableNumber][cellNumber]}
              />
            </td>
          {/each}
          <td rowspan="2" class="average bottom"
            >{calcTableAverage(tables[tableNumber])}</td
          >
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
</div>

<div class="buttons">
  <button class="btn-add" on:click={createTable}>➕</button>
  <button class="btn-del" on:click={deleteTable}>➖</button>
</div>

<style>
  .main-table {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  th,
  .average {
    text-align: center;
    font-size: 1.5em;
    font-family: var(--primary-font);
    padding: 0.25em 0.5em;
  }

  table {
    display: block;
    border-collapse: collapse;
    border: 3px solid var(--color-blue);
    border-radius: 0.5em;
  }

  input {
    font-size: 1.25em;
    font-family: var(--seconday-font);
    background-color: var(--color-dark);
    color: var(--color-light);
    text-align: center;
    width: 2.5em;
    height: 2.5em;
    outline: none;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  /* Firefox */
  input[type="number"] {
    -moz-appearance: textfield;
  }

  .buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 1.5em;
  }

  button {
    font-size: 1.5em;
    padding: 0.25em 0.25em;
  }

  .btn-add {
    background-color: var(--color-green);
    border-radius: 0.25em 0 0 0.25em;
  }

  .btn-del {
    background-color: var(--color-red);
    border-radius: 0 0.25em 0.25em 0;
  }
</style>
