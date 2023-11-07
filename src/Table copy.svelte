<script>
    //@ts-nocheck
import { ActiveTable } from "active-table";
import { Button, Modal } from 'flowbite-svelte';
  import { onDestroy, onMount } from "svelte";

let defaultModal = false;
let ok = false;

var content = [["A","B"],[1,2],[3,4],[5,6]];

var oldTable = []


const abortController = new AbortController();

// window.addEventListener('load', function() {
// // Your code to run after everything has loaded
// tableListener()
// });

function handleInput(event) {
    if (event.keyCode == 13){
    event.preventDefault();
  }
}

// const myComponent = document.getElementById('activetable');
var tabler;
onMount(()=>{
tabler.onContentUpdate = (contentUpdate) => { 
tableListener();
//console.log(contentUpdate); 
};
ok = true;
})

onDestroy(()=>{
    ok = false;
});

function dbHandler(){
 
// Access the cells within the row
const cells = row.querySelectorAll('td');
// console.log(cells)
console.log(row)
//debugger
// Access and log the content of the cells
// const content1 = cells[0].innerHTML;
// console.log(content1);

defaultModal  =true;


}

function removeAllChildEventListeners(parentElement) {
  const childElements = parentElement.children;

  for (const child of childElements) {
    const clonedNode = child.cloneNode(true);
    child.replaceWith(clonedNode);
  }
}


function tableListener(){
if (!ok || !tabler){
    console.log("NOT OK")
    return;
}
removeAllChildEventListeners(tabler);
const rows= tabler.shadowRoot.querySelector('table').querySelectorAll('tr')

// Iterate over the rows and add a double-click event listener
Array.from(rows).forEach((row, index) => {
try{
    row.removeEventListener('dblclick',dbHandler);
    // row.removeEventListener('dblclick');
    // row.addEventListener("dblclick", ()=>abortController.abort());
}
catch{
    console.log("CAUGHT!")
}
row.addEventListener('dblclick', ()=>{
    
// Access the cells within the row
const cells = row.querySelectorAll('td');
// console.log(cells)
console.log(row)
//debugger
// Access and log the content of the cells
// const content1 = cells[0].innerHTML;
// console.log(content1);

defaultModal  =true;

});  // ,{ once: true }
});
}





</script>
<div>

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

displayAddNewRow={true}


/>



<Modal id="top-center-modal" title="Terms of Service" bind:open={defaultModal} autoclose outsideclose >
 
    <p></p>
    <p></p>
  
  
  
    <svelte:fragment slot="footer">
    <Button on:click={() => alert('Handle "success"')}>I accept</Button>
    <Button on:click={defaultModal=false} color="alternative">Decline</Button>
  </svelte:fragment>
</Modal>

</div>
<style>






</style>