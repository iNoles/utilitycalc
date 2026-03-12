<script>
  let weight = $state(0);
  let drinks = $state(0);
  let hours = $state(0);
  let gender = $state("male");

  const r = { male: 0.73, female: 0.66 };

  let alcoholOz = $derived(drinks * 0.6);

  let bac = $derived(
    weight > 0 && drinks > 0
      ? (
          (alcoholOz * 5.14) / (weight * r[gender]) -
          0.015 * hours
        ).toFixed(3)
      : "—"
  );
</script>

<div class="w-full bg-white shadow-2xl rounded-2xl p-8 space-y-6 border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">BAC Calculator</h1>

  <div class="space-y-4">
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="body-weight">Body Weight (lbs)</label>
      <input
        type="number"
        id="body-weight"
        bind:value={weight}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-red-500 focus:outline-none"
        placeholder="Enter weight"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="drink">Number of Drinks</label>
      <input
        type="number"
        id="drink"
        bind:value={drinks}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-red-500 focus:outline-none"
        placeholder="Standard drinks"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="hours">Hours Since First Drink</label>
      <input
        type="number"
        id="hour"
        bind:value={hours}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-red-500 focus:outline-none"
        placeholder="Hours"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="gender">Gender</label>
      <select
        id="gender"
        bind:value={gender}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-red-500 focus:outline-none"
      >
        <option value="male">Male</option>
        <option value="female">Female</option>
      </select>
    </div>
  </div>

  <div class="bg-red-50 border border-red-200 rounded-xl p-6 text-center shadow-inner">
    <p class="text-sm text-red-700 font-medium">Estimated BAC</p>
    <p class="text-4xl font-bold text-red-900 mt-1">{bac}</p>
  </div>
</div>
