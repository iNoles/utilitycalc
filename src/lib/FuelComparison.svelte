<script>
  let mpgCurrent = $state(0);
  let mpgNew = $state(0);
  let milesPerYear = $state(0);
  let fuelPrice = $state(0);

  let costCurrent = $derived(
    mpgCurrent > 0
      ? ((milesPerYear / mpgCurrent) * fuelPrice).toFixed(2)
      : "—"
  );

  let costNew = $derived(
    mpgNew > 0
      ? ((milesPerYear / mpgNew) * fuelPrice).toFixed(2)
      : "—"
  );

  let savings = $derived(
    costCurrent !== "—" && costNew !== "—"
      ? (costCurrent - costNew).toFixed(2)
      : "—"
  );
</script>

<div class="w-full bg-white shadow-2xl rounded-2xl p-8 space-y-6 border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">
    Fuel Savings Comparison
  </h1>

  <div class="space-y-4">
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="current-mpg">
        Average MPG (Current Vehicle)
      </label>
      <input
        type="number"
        id="current-mpg"
        bind:value={mpgCurrent}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-indigo-500 focus:outline-none"
        placeholder="e.g., 22"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="new-mpg">
        Average MPG (New Vehicle)
      </label>
      <input
        type="number"
        id="new-mpg"
        bind:value={mpgNew}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-indigo-500 focus:outline-none"
        placeholder="e.g., 32"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="miles">
        Miles Driven Per Year
      </label>
      <input
        type="number"
        id="miles"
        bind:value={milesPerYear}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-indigo-500 focus:outline-none"
        placeholder="e.g., 12000"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="fuel-price">
        Average Fuel Price ($)
      </label>
      <input
        type="number"
        id="fuel-price"
        step="0.01"
        bind:value={fuelPrice}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-indigo-500 focus:outline-none"
        placeholder="e.g., 3.45"
      />
    </div>
  </div>

  <div class="bg-indigo-50 border border-indigo-200 rounded-xl p-6 shadow-inner space-y-3">
    <div class="flex justify-between text-sm text-gray-700">
      <span>Yearly Cost (Current Vehicle):</span>
      <span class="font-semibold">${costCurrent}</span>
    </div>

    <div class="flex justify-between text-sm text-gray-700">
      <span>Yearly Cost (New Vehicle):</span>
      <span class="font-semibold">${costNew}</span>
    </div>

    <div class="flex justify-between text-sm text-indigo-700 text-lg font-bold pt-2">
      <span>Yearly Savings:</span>
      <span>${savings}</span>
    </div>
  </div>
</div>
