<script>
    //@ts-ignore
    import { Tabs, Tab, TabList, TabPanel } from 'svelte-tabs';
  import Fahrzeuge from './Fahrzeuge.svelte';
  </script> 
   <div class="w-full tabs top-0 right-0 mt-3 mr-3 items-center space-x-4">
  <Tabs>
    <TabList class="w-full tabs">
      <Tab >Fahrzeuge</Tab>
      <Tab >Zubehör</Tab>
      <Tab >Wartung</Tab>
      <Tab >Mitarbeiter</Tab>
    </TabList>
   
    <TabPanel>
      <h2>Fahrzeuge</h2>
      <Fahrzeuge/>
    </TabPanel>
   
    <TabPanel>
      <h2>Zubehör</h2>
    </TabPanel>
   
    <TabPanel>
      <h2>Wartung</h2>
    </TabPanel>


    <TabPanel>
        <h2>Mitarbeiters</h2>
      </TabPanel>
  </Tabs>
</div>



  <style>
    .tabs {
        border: 1px;
        border-color: beige;
        width: 100% !important;
        position: absolute;
    }

  </style>