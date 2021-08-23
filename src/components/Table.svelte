<script lang="ts">
  let tables: number[][] = [Array(10).fill(null)];

  const calcTableAverage = (cellValues: number[]) => {
    const total = cellValues.reduce((x, y) => x + y);
    return total / 10;
  };

  const calcLotAverage = (tables: number[][], index: number) => {
    let lotAverage = 0;

    for (let i = 0; i < index + 1; i++) {
      console.log(calcTableAverage(tables[i]));
      lotAverage += calcTableAverage(tables[i]) / (index + 1);
    }
    return lotAverage.toFixed(1);
  };

  const createTable = () => {
    tables = [...tables, Array(10).fill(null)];
  };

  const deleteTable = () => {
    if (tables.length > 1) {
      tables.pop();
      tables = tables;
    }
  };
</script>

<div class="main-table">
  <table>
    <thead>
      <tr>
        <th colspan="5">weights</th>
        <th>avg</th>
        <th>lot</th>
      </tr>
    </thead>
    <tbody>
      {#each Array(tables.length) as _, tableNumber}
        <tr class="top">
          {#each Array(5) as _, cellNumber}
            <td>
              <input
                class:blue-row={tableNumber % 2}
                type="number"
                bind:value={tables[tableNumber][cellNumber]}
                placeholder="0"
              />
            </td>
          {/each}
          <td
            rowspan="2"
            class="average bottom"
            class:blue-row={tableNumber % 2}
            >{calcTableAverage(tables[tableNumber])}</td
          >
          <td class:blue-row={tableNumber % 2} rowspan="2" class="average"
            >{calcLotAverage(tables, tableNumber)}</td
          >
        </tr>
        <tr>
          {#each Array(5) as _, cellNumber}
            <td>
              <input
                class:blue-row={tableNumber % 2}
                placeholder="0"
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
    padding: 0 0.25em;
  }

  table {
    display: block;
    border-collapse: collapse;
    border: 0.25em solid var(--color-blue);
    border-radius: 1em;
  }

  .blue-row {
    background-color: var(--color-blue);
    color: var(--color-dark);
  }

  .blue-row::placeholder {
    color: var(--color-dark);
  }

  input {
    font-size: 1.25em;
    font-family: var(--seconday-font);
    background-color: transparent;
    color: var(--color-light);
    text-align: center;
    width: 2.5em;
    height: 2.5em;
    outline: none;
    padding: 0.25em;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  input[type="number"] {
    -moz-appearance: textfield;
  }

  input::placeholder {
    color: var(--color-light);
  }

  input:focus::placeholder {
    color: transparent;
    border-bottom: 0.15em solid var(--color-blue);
  }

  .blue-row:focus::placeholder {
    border-bottom: 0.15em solid var(--color-dark);
  }

  .buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 1.5em;
    margin-bottom: 1.5em;
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
