<script lang="ts">
    import { currentUser, errorMessage, pocketbase } from "./lib/pocketbase";
   
  
    async function handleSignOut() {
        try {
    pocketbase.authStore.clear();
  } catch (error) {
    errorMessage(error);
  }
    }
  </script>
  
  <div  class="flex z-10 flex-row absolute top-0 right-0 mt-1 mr-3 items-center space-x-4">
    <p>{$currentUser?.email}</p>
    <button
      class="group relative flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 mt-2"
      on:click={handleSignOut}
    >
      <span class="absolute inset-y-0 left-0 flex items-center pl-3" />
      Sign Out
    </button>
  </div>

  <style>

  </style>