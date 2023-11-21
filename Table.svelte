<script>
  import { Grid } from "ag-grid-community";
  import { onMount } from "svelte";
  import { data } from "./data.json";
  import RowDetails from "./RowDetails";
  import { getContext, setContext } from "svelte";

  const { open, close } = getContext("simple-modal");
  let table, selectedRow, grid;

  let columnDefs = Object.keys(data[0]).map(e => ({
    headerName: e,
    field: e,
    minWidth: 130,
    filter: "agNumberColumnFilter",
    sortable: true
    // resizable: true
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
    params.api.sizeColumnsToFit();
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

  const onPrev = (data, updateData) => {
    let event = gridOptions.api.getDisplayedRowAtIndex(data.rowIndex - 1);
    if (event) updateData(event);
  };
  const onNext = (data, updateData) => {
    let event = gridOptions.api.getDisplayedRowAtIndex(data.rowIndex + 1);
    if (event) updateData(event);
  };
  const onClose = () => console.log("onprev");

  function handleRowClick(event) {
    open(RowDetails, { event, onPrev, onNext, onClose });
  }

  onMount(() => {
    if (table) grid = new Grid(table, gridOptions);
  });
</script>


<div bind:this={table} class="w-screen h-screen ag-theme-alpine"/>
