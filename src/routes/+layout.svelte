<script lang="ts">
  import './layout.css';
  import favicon from '$lib/assets/favicon.svg';
  import { base } from '$app/paths';

  let { children } = $props();
  let mobileOpen = $state(false);
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<div class="min-h-screen bg-gray-100 text-gray-900 flex flex-col">

  <header class="bg-white border-b border-gray-200">
    <div class="max-w-4xl mx-auto px-6 py-4 flex items-center justify-between">

      <a href="/" class="text-2xl font-semibold tracking-tight text-gray-900">
        UtilityCalc
      </a>

      <nav class="hidden sm:flex gap-6 text-sm font-medium text-gray-700">
        <a href="{base}/gas-mileage" class="hover:text-gray-900">Gas Mileage</a>
        <a href="{base}/fuel-comparison" class="hover:text-gray-900">Fuel Savings</a>
        <a href="{base}/amortization" class="hover:text-gray-900">Amortization</a>
        <a href="{base}/bac" class="hover:text-gray-900">BAC</a>
      </nav>

      <button
        class="sm:hidden p-2 rounded-md border border-gray-300 text-gray-700"
        onclick={() => (mobileOpen = !mobileOpen)}
        aria-label="Toggle menu"
      >
        {#if mobileOpen}
          ✕
        {:else}
          ☰
        {/if}
      </button>
    </div>

    {#if mobileOpen}
      <nav class="sm:hidden bg-white border-t border-gray-200 px-6 py-4 space-y-3 text-gray-700 text-base">
        <a href="{base}/gas-mileage" class="block hover:text-gray-900">Gas Mileage</a>
        <a href="{base}/fuel-comparison" class="block hover:text-gray-900">Fuel Savings</a>
        <a href="{base}/amortization" class="block hover:text-gray-900">Amortization</a>
        <a href="{base}/bac" class="block hover:text-gray-900">BAC</a>
      </nav>
    {/if}
  </header>

  <main class="max-w-3xl mx-auto p-6 flex-1">
    {@render children()}
  </main>
</div>
