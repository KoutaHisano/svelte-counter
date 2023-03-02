<script lang="ts">
  import { createEventDispatcher, onMount } from "svelte";
  import type { CounterType } from "../Counter";

  export let counter: CounterType;

  const dispatch = createEventDispatcher();

  onMount(() => {
    dispatch("update", { count: counter.count });
  });

  function increment() {
    counter.count++;
    dispatch("update", { count: counter.count });
  }

  function decrement() {
    counter.count--;
    dispatch("update", { count: counter.count });
  }

  function reset() {
    counter.count = 0;
    dispatch("update", { count: counter.count });
  }

  function remove() {
    dispatch("remove");
  }
</script>

<div>
  <div class="counter-box">
    <form class="title-form">
      <input type="text" placeholder="タイトル入力" />
    </form>
    <button class="minus-button" on:click={decrement}>-</button>
    <span>{counter.count}</span>
    <button class="plus-button" on:click={increment}>+</button>
    <button class="reset-button" on:click={reset}>reset</button>
    <button class="del-button" on:click={remove}>消</button>
  </div>
</div>
