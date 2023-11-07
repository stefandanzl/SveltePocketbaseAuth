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
let isLoaded = false;

onMount(() => {
  getData().then((output)=>{ tabler.updateContent(output);}).then(()=>{})
  isLoaded = true;
});

async function getData(){
    try {
    const records = await pb.collection('dummyusers').getFullList({
      sort: '-created',
    });
    // Now you can work with the 'records' data
    let output = [["Beschreibung","Fahrzeug","Art"]]

    for (var r in records){
        // console.log("r",r)
        output.push([records[r].firstName,records[r].lastName,records[r].email,records[r].age,records[r].birthDate,records[r].phone])
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
    <button class="buttons" on:click={setR}>DATA</button>


    {#if isLoaded}
<!-- svelte-ignore a11y-no-static-element-interactions -->
    <active-table on:keydown={handleInput} id="active-table" bind:this={tabler}
    
    content={content}

auxiliaryStyle={
    `::-webkit-scrollbar {
      width: 10px;
      height: 10px;
    }
    ::-webkit-scrollbar-thumb {
      background-color: #54a7ff;
      border-radius: 5px;
    }`}

displayAddNewColumn={false}


stickyHeader={true}
isHeaderTextEditable= {false}
customColumnsSettings={[
    { "headerName": "Beschreibung",  "availableDefaultColumnTypes": ["Text"],"defaultText": "Neues Auto"},
    { "headerName": "Fahrzeug", "availableDefaultColumnTypes": ["Text"], "defaultColumnTypeName": "Text"},
    { "headerName": "Type",  "defaultColumnTypeName": "Select"},
    { "headerName": "Date Created",  "defaultColumnTypeName": "Date d-m-y" }
  ]}

rowHoverStyles={{"style":{"backgroundColor": "#d6d6d630", "transitionDuration": "0.1s"}}}
    

cellStyle={{"color": "white", "borderRight": "1px solid #00000029"}}
columnResizerColors={{"click": "#727272"}}
stripedRows={{"odd": {"backgroundColor": "#4f4f4f"}, "even": {"backgroundColor": "#373737"}}}
headerStyles={{"default": {"backgroundColor": "#2d2d2d"}, "hoverColors": {"backgroundColor": "#353535"}}}
headerIconStyle={{
  "filterColor": "brightness(0) saturate(100%) invert(98%) sepia(2%) saturate(6%) hue-rotate(76deg) brightness(100%) contrast(104%)"
}}
frameComponentsStyles={{
  "style": {"hoverColors": {"backgroundColor": "#5f5f5f"}},
  "inheritHeaderColors": true
}}

tableStyle={{
  "borderRadius": "10px",
  "boxShadow": "rgb(172 172 172 / 17%) 0px 0.5px 1px 0px",
  "width":"90%","border": "unset", "backgroundColor": "black"
}}

displayAddNewRow={false}

    
    />
{/if}



</div>
<style>

</style>