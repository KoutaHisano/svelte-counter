<script lang="ts">
  import type { CounterType } from "./Counter";
  import Counter from "./lib/Counter.svelte";
  import { v4 as uuidv4 } from "uuid";

  let counters: CounterType[] = [];
  let addCounter = () => {
    const id = uuidv4();
    counters = [...counters, { id, title: "", count: 0 }];
  };

  let removeCounter = (id: string) => {
    counters = counters.filter((counter) => counter.id !== id);
  };

  let updateCounter = (id: string, count: number) => {
    counters = counters.map((counter) =>
      counter.id === id ? { ...counter, count } : counter,
    );
  };

  let totalCount = (counters: CounterType[]) => {
    let total = 0;
    for (const counter of counters) {
      total += counter.count;
    }
    return total;
  };
</script>

<h1>svelte カウンター</h1>
<div>
  <button class="counterAdd" on:click={addCounter}>カウンターを追加</button>
</div>

<div>
  {#each counters as counter (counter.id)}
    <Counter
      {counter}
      on:update={(e) => updateCounter(counter.id, e.detail.count)}
      on:remove={() => removeCounter(counter.id)}
    />
  {/each}
</div>

<div>
  <p>合計: {totalCount(counters)}</p>
</div>
