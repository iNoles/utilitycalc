<script>
  import GasMileage from "$lib/GasMileage.svelte";
</script>

<section class="space-y-4 mb-8">
  <h1 class="text-3xl font-bold text-gray-900">Gas Mileage Calculator</h1>

  <p class="text-gray-700 leading-relaxed">
    This calculator estimates your vehicle’s real‑world miles per gallon (MPG)
    based on the distance you drive and the fuel you use. It helps you track
    how efficiently your vehicle performs over time and can highlight changes
    that may signal maintenance needs.
  </p>

  <p class="text-gray-700 leading-relaxed">
    Knowing your current MPG also gives you a baseline for comparing vehicles
    when considering a more fuel‑efficient model. It’s a practical way to
    understand how your driving habits and fuel costs affect your budget.
  </p>

  <p class="text-gray-700 leading-relaxed">
    For long‑term savings insights, pair this with the Fuel Savings Comparison
    Calculator to estimate how much you could save each year by upgrading to a
    more efficient vehicle.
  </p>
</section>

<GasMileage />
