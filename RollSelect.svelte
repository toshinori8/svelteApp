<script>
  import { onMount } from "svelte";
  import { createEventDispatcher } from "svelte";
  import MobileSelect from "mobile-select";
  export let values = ["1", "2"];
  export let show;
  export let hide;

  const dispatch = createEventDispatcher();

  let element, select;

  onMount(() => {
    select = new MobileSelect({
      trigger: "#roll",
      title: "Select Value",
      cancelBtnText: "Cancel",
      ensureBtnText: "Done",
      wheels: [{ data: values }],
      triggerDisplayData: false,
      callback: function(indexArr, data) {
        dispatch("selected", { data }); //Returns the selected json data
      }
    });
    show = () => select.show();
    hide = () => select.hide();
  });
</script>


<div id="roll" class=""></div>