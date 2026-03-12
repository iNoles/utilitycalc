<script>
  let miles = $state(0);
  let gallons = $state(0);

  let mpg = $derived(
    gallons > 0 ? (miles / gallons).toFixed(2) : "—"
  );
</script>

<div class="w-full bg-white shadow-2xl rounded-2xl p-8 space-y-6 border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">Gas Mileage Calculator</h1>

  <div class="space-y-4">
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="miles-input">Miles Driven</label>
      <input
        type="number"
        id="miles-input"
        bind:value={miles}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-blue-500 focus:outline-none"
        placeholder="Enter miles"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="fuel-input">Gallons Used</label>
      <input
        type="number"
        id="fuel-input"
        bind:value={gallons}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-blue-500 focus:outline-none"
        placeholder="Enter gallons"
      />
    </div>
  </div>

  <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
    <p class="text-sm text-blue-700 font-medium">Miles Per Gallon</p>
    <p class="text-4xl font-bold text-blue-900 mt-1">{mpg}</p>
  </div>
</div>
