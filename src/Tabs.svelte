<script>
    //@ts-ignore
    import { Tabs, Tab, TabList, TabPanel } from 'svelte-tabs';
  import Fahrzeuge from './Fahrzeuge.svelte';
  import Wartung from './Wartung.svelte';
  import Mitarbeiter from './Mitarbeiter.svelte';
  import Zubehor from './Zubehor.svelte';
  </script> 
   <div class="w-full tabs top-0 right-0 mt-3 mr-3 items-center space-x-4">
  <Tabs>
    <TabList>
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
      <Zubehor />
    </TabPanel>
   
    <TabPanel>
      <h2>Wartung</h2>
      <Wartung />
    </TabPanel>


    <TabPanel>
        <h2>Mitarbeiters</h2>
        <Mitarbeiter />
      </TabPanel>
  </Tabs>
</div>



  <style>
    .tabs {
        border: 1px;
        border-color: beige;
        width: 100% !important;
        position: absolute;
        max-height: 100% !important;
        
    }

  </style>