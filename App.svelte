<script>
  import Button from "./Button.svelte";
  import Modal from "./Modal.svelte";
  import { getContext, setContext } from "svelte";
  import { onMount } from "svelte";
  import RowDetails from "./RowDetails.svelte";
  import { data } from "./data.json";
  import { gestures } from "@composi/gestures";
  import Table from "./Table";
  import RollSelect from "./RollSelect";
  import CheckboxSelect from "./checkbox-select";
  gestures();

  let show, hide;
</script>

<CheckboxSelect />


<!-- <RollSelect on:selected={(data) => console.log('data')} bind:show bind:hide/> -->

<!-- <Modal>
  <Table />
</Modal> -->
<svelte:head>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/mobile-select@1.1.2/mobile-select.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/ag-grid/23.0.2/styles/ag-theme-alpine.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/ag-grid/23.0.2/styles/ag-grid.min.css">
    <link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet">
</svelte:head>



<!-- <script>
  import { Grid } from "ag-grid-community";
  import { onMount } from "svelte";
  import { data } from "./data.json";

  let table, selectedRow;

  let columnDefs = Object.keys(data[0]).map(e => ({
    headerName: e,
    field: e,
    // minWidth: 150,
    filter: "agNumberColumnFilter",
    sortable: true,
    resizable: true
  }));

  var rowData = data;

  var gridOptions = {
    defaultColDef: {
      resizable: true
    },
    columnDefs: columnDefs,
    rowData: rowData,
    onFirstDataRendered: onFirstDataRendered,

    onGridSizeChanged: onGridSizeChanged,
    onRowClicked: handleRowClick
  };

  function onFirstDataRendered(params) {
    // params.api.sizeColumnsToFit();
    autoSizeAll(false);
  }

  function autoSizeAll(skipHeader) {
    var allColumnIds = [];
    gridOptions.columnApi.getAllColumns().forEach(function(column) {
      allColumnIds.push(column.colId);
    });

    gridOptions.columnApi.autoSizeColumns(allColumnIds, skipHeader);
  }

  function onGridSizeChanged(params) {
    // get the current grids width
    var gridWidth = table.offsetWidth;

    // keep track of which columns to hide/show
    var columnsToShow = [];
    var columnsToHide = [];

    // iterate over all columns (visible or not) and work out
    // now many columns can fit (based on their minWidth)
    var totalColsWidth = 0;
    var allColumns = params.columnApi.getAllColumns();
    for (var i = 0; i < allColumns.length; i++) {
      var column = allColumns[i];
      totalColsWidth += column.getMinWidth();
      if (totalColsWidth > gridWidth) {
        columnsToHide.push(column.colId);
      } else {
        columnsToShow.push(column.colId);
      }
    }

    // show/hide columns based on current grid width
    params.columnApi.setColumnsVisible(columnsToShow, true);
    params.columnApi.setColumnsVisible(columnsToHide, false);

    // fill out any available space to ensure there are no gaps
    params.api.sizeColumnsToFit();
  }

  function handleRowClick(e) {}

  onMount(() => {
    if (table) new Grid(table, gridOptions);
  });
</script>

<svelte:head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/ag-grid/23.0.2/styles/ag-theme-alpine.min.css">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/ag-grid/23.0.2/styles/ag-grid.min.css">
  <link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet">
</svelte:head>

<div bind:this={table} class="w-screen h-screen ag-theme-alpine"/> -->

