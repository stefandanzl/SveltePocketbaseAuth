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
    const records = await pb.collection('maintenance').getFullList({
      sort: '-created',
    });
    // Now you can work with the 'records' data
    let output = [["Beschreibung","Fahrzeug","Art"]]

    for (var r in records){
        // console.log("r",r)
        output.push([records[r].description,records[r].vehicle,records[r].type])
    }
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
    <button class="buttons absolute left-40" on:click={setR}>DATA</button>
<!-- svelte-ignore a11y-no-static-element-interactions -->
    <active-table on:keydown={handleInput} id="active-table" bind:this={tabler}
    
    content={content}

    displayAddNewColumn={false}
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
isHeaderTextEditable= {false}
customColumnsSettings={[
    { "headerName": "Kennzeichen",  "availableDefaultColumnTypes": ["Text"],"defaultText": "Neues Auto"},
    { "headerName": "Marke", "availableDefaultColumnTypes": ["Text"], "defaultColumnTypeName": "text"},
    { "headerName": "Type",  "defaultColumnTypeName": "Select",  },
    { "headerName": "Date Created",  "defaultColumnTypeName": "Date d-m-y" }
  ]}

rowHoverStyles={{"style":{"backgroundColor": "#d6d6d630", "transitionDuration": "0.1s"}}}
    

    
    
    />




</div>
<style>

</style>