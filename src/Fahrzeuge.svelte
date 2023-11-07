<script>
    //@ts-nocheck
import { ActiveTable } from "active-table";
import { onMount } from "svelte";
  
  import {pb} from "./lib/pocketbase.ts";

  function handleInput(event) {
    if (event.keyCode == 13){
    event.preventDefault();
  }
}

let tabler;


onMount(() => {
  getData().then((output)=>{ tabler.updateContent(output);})
});

async function getData(){
    try {
    const records = await pb.collection('vehicles').getFullList({
      sort: '-created',
    });

    // Now you can work with the 'records' data
    console.log(records);

    let output = [["Beschreibung","Marke","Type"]]
    // let output = [["","",""]]

    for (var r in records){
        console.log("r",r)
        output.push([records[r].kennZeichen,records[r].make,records[r].model])
    }

    
    
    // tabler.updateContent(output);
    return output;
    
  } catch (error) {
    // Handle any errors that may occur during the data retrieval
    console.error(error);
  }
}

function setR(){
    getData().then((output)=>{ tabler.updateContent(output);})
}



var content = []


</script>
<div>
    <button class="buttons" on:click={setR}>DATA</button>
<!-- svelte-ignore a11y-no-static-element-interactions -->
    <active-table on:keydown={handleInput} id="active-table" bind:this={tabler}
    
    content={content}
    displayAddNewRow={false}
auxiliaryStyle={
    `::-webkit-scrollbar {
      width: 10px;
      height: 10px;
    }
    ::-webkit-scrollbar-thumb {
      background-color: #54a7ff;
      border-radius: 5px;
    }`}

stickyHeader={true}

displayAddNewColumn={false}


customColumnsSettings={[
    { "headerName": "Kennzeichen",  "availableDefaultColumnTypes": ["Text"],"defaultText": "Neues Auto", "cellStyle": {"width": "150px"}, "isHeaderTextEditable": false },
    { "headerName": "Marke", "availableDefaultColumnTypes": ["Text"], "defaultColumnTypeName": "text", "isHeaderTextEditable": false },
    { "headerName": "Type",  "defaultColumnTypeName": "Select", "isHeaderTextEditable": false },
    { "headerName": "Date Created", "cellStyle": {"backgroundColor": "#f1f1f1"}, "defaultColumnTypeName": "Date d-m-y", "isHeaderTextEditable": false }
  ]}

rowHoverStyles={{"style":{"backgroundColor": "#d6d6d630", "transitionDuration": "0.05s"}}}
    

    
    
    />




</div>
<style>

</style>