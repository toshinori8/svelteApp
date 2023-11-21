<script>
  import _ from "lodash";
  import { createEventDispatcher } from "svelte";
  import { getContext } from "svelte";
  import { gestures } from "@composi/gestures";

  import FaAngleUp from "svelte-icons/fa/FaAngleUp.svelte";
  import FaAngleDown from "svelte-icons/fa/FaAngleDown.svelte";

  const dispatch = createEventDispatcher();

  const { close } = getContext("simple-modal");

  export let onPrev = () => {};
  export let onNext = () => {};
  export let event = {};
  const next = () => onNext(event, updateData);
  const prev = () => onPrev(event, updateData);

  function updateData(newData) {
    event = newData;
  }
</script>

<div class="h-full w-full bg-gray-100 relative">
  <div class="w-full px-4 py-3 border-b flex items-center sticky top-0 bg-gray-200">
    <span class="w-10 flex">
      <span class="inline-block mr-2 cursor-pointer" style="width:10px" on:click={prev}><FaAngleUp /></span>
      <span class="inline-block cursor-pointer" style="width:10px" on:click={next}><FaAngleDown /></span>
    </span>
    <span class="mx-4 inline-block truncate test-xs">{_.get(event.data, 'name')}</span>
  </div>

  <div class="py-5 px-10" on:swipeleft={next} on:swiperight={prev} on:dbltap={close}>
    <div class="font-medium text-2xl my-8">{_.get(event.data, 'name')}</div>
    {#each _.keysIn(event.data) as key}
      <div class="mb-6">
        <div class="text-gray-600 uppercase mb-1 text-sm">{key}</div>
        <div class="text-lg">{@html _.get(event.data, key)}</div>
      </div>
    {/each}
  </div>
</div>