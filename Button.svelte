<script>
	import Helo from "./helo.svelte";
	let count = 0;
	import RowDetails from "./RowDetails.svelte";

	let label;
	export let data;

	function handleClick() {
	  count += 1;
	}
	import { getContext, setContext } from "svelte";
	import { onMount } from "svelte";

	const { open, close } = getContext("simple-modal");

	const onPrev = () => console.log("onprev");
	const onNext = () => console.log("onprev");
	const onClose = () => console.log("onprev");
	let oppp = () => open(RowDetails, { data, onPrev, onNext, onClose });
</script>

<style>
	button {
	  background: #ff3e00;
	  color: white;
	  border: none;
	  padding: 8px 12px;
	  border-radius: 2px;
	}
</style>

<button on:click={oppp}>
  Clicked {count} {count === 1 ? 'time' : 'times'}
</button>