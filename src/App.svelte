<script lang="ts">
  import LoginScreen from "./LoginScreen.svelte";
  import { currentUser } from "./lib/pocketbase";
  import UserScreen from "./UserScreen.svelte";
  import Tabs from "./Tabs.svelte";
</script>

{#if !$currentUser}
  <LoginScreen />
{:else}
  <UserScreen />
  <Tabs />
{/if}