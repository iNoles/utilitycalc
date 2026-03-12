<script>
  import FuelComparison from "$lib/FuelComparison.svelte";
</script>

<section class="space-y-4 mb-8">
  <h1 class="text-3xl font-bold text-gray-900">Fuel Savings Comparison</h1>

  <p class="text-gray-700 leading-relaxed">
    This tool compares the yearly fuel cost of your current vehicle with a more
    fuel‑efficient option. By entering your average MPG, annual mileage, and
    fuel price, you can estimate how much you spend on fuel each year and how
    much you could save by switching vehicles.
  </p>

  <p class="text-gray-700 leading-relaxed">
    It’s especially useful when evaluating hybrids, newer models with better
    efficiency, or any upgrade where long‑term fuel savings matter. The results
    help you understand the financial impact of fuel economy over time.
  </p>

  <p class="text-gray-700 leading-relaxed">
    Use this alongside the Gas Mileage Calculator to get a complete picture of
    your current vehicle’s performance before comparing alternatives.
  </p>
</section>

<FuelComparison />
