<script lang="ts">
  let tables: number[][] = [Array(10).fill(null)];

  const calcTableAverage = (cellValues: number[]) => {
    const total = cellValues.reduce((x, y) => x + y);
    return total / 10;
  };

  // calculates the average of each table average
  const calcLotAverage = (tables: number[][], index: number) => {
    let lotAverage = 0;

    for (let i = 0; i < index + 1; i++) {
      lotAverage += calcTableAverage(tables[i]) / (index + 1);
    }
    return lotAverage.toFixed(1);
  };

  const addTable = () => {
    tables = [...tables, Array(10).fill(null)];
  };

  const deleteTable = () => {
    if (tables.length > 1) {
      tables.pop();
      tables = tables;
    }
  };
</script>

<div class="my-4 flex justify-center">
  <table>
    <thead>
      <tr class="capitalize">
        <th colspan="5" class="text-lg capitalize">weights</th>
        <th>avg</th>
        <th>lot</th>
      </tr>
    </thead>
    <tbody>
      {#each Array(tables.length) as _, tableNumber}
        <tr class:bg-neutral-200={tableNumber % 2}>
          {#each Array(5) as _, cellNumber}
            <td class="border border-black p-2">
              <input
                class:bg-neutral-200={tableNumber % 2}
                class="w-12 text-center focus:outline-none sm:w-16 md:w-24"
                type="number"
                bind:value={tables[tableNumber][cellNumber]}
                placeholder="0"
              />
            </td>
          {/each}
          <td rowspan="2" class="w-12 text-center sm:w-16 md:w-24">
            <p>{calcTableAverage(tables[tableNumber])}</p>
          </td>
          <td rowspan="2" class="w-12 text-center">
            <p>{calcLotAverage(tables, tableNumber)}</p>
          </td>
        </tr>
        <tr class:bg-neutral-200={tableNumber % 2}>
          {#each Array(5) as _, cellNumber}
            <td class="border border-black p-2">
              <input
                class="w-12 text-center focus:outline-none sm:w-16 md:w-24"
                class:bg-neutral-200={tableNumber % 2}
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

<div class="flex justify-center gap-2">
  <button class="aspect-square w-8 bg-green-400" on:click={addTable}>➕</button>
  <button class="aspect-square w-8 bg-red-400" on:click={deleteTable}>➖</button
  >
</div>
