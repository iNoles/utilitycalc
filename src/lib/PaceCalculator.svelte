<script lang="ts">
  // User-controlled state
  let mode = $state<'pace' | 'time' | 'distance'>('pace');
  let unit = $state<'mi' | 'km'>('mi');

  let distance = $state(1);
  let timeMin = $state(0);
  let timeSec = $state(0);
  let paceMin = $state(0);
  let paceSec = $state(0);

  // Conversion helpers
  const kmToMiles = (km: number) => km * 0.621371;
  const milesToKm = (mi: number) => mi / 0.621371;

  // Convert distance input to miles for internal math
  const distanceInMiles = $derived(() => {
    return unit === "mi" ? distance : kmToMiles(distance);
  });

  // Convert pace input to minutes per mile for internal math
  const pacePerMile = $derived(() => {
    const p = paceMin + paceSec / 60;
    return unit === "mi" ? p : p / 0.621371;
  });

  // Helpers
  const toMinutes = (min: number, sec: number) => min + sec / 60;

  const fromMinutes = (m: number) => {
    const min = Math.floor(m);
    const sec = Math.round((m - min) * 60);
    return { min, sec };
  };

  // Pure compute functions
  const computePace = () => {
    const total = toMinutes(timeMin, timeSec);
    return distanceInMiles > 0 ? fromMinutes(total / distanceInMiles) : null;
  };

  const computeTime = () => {
    if (pacePerMile() <= 0 || distanceInMiles() <= 0) return null;
    return fromMinutes(pacePerMile() * distanceInMiles());
  };

  const computeDistance = () => {
    const total = toMinutes(timeMin, timeSec);
    return pacePerMile > 0 ? total / pacePerMile : null;
  };

  // Derived values
  let result = $derived(() => {
    if (mode === "pace") {
      const r = computePace();
      return r ?? { min: 0, sec: 0 };
    }

    if (mode === "time") {
      const r = computeTime();
      return r ?? { min: 0, sec: 0 };
    }

    // distance mode
    const d = computeDistance();
    return d ?? 0;
  });

  // Convert distance result to selected unit
  let resultDistance = $derived(() => {
    const d = computeDistance();
    if (d === null) return "—";
    return unit === "mi" ? `${d.toFixed(2)} mi` : `${milesToKm(d).toFixed(2)} km`;
  });
</script>

<div class="w-full bg-white shadow-2xl rounded-2xl p-8 space-y-6 border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">Pace Calculator</h1>

  <!-- Unit Toggle -->
  <div class="flex justify-center gap-3 mb-4">
    <button
      class="px-3 py-1 rounded-md border text-sm"
      class:bg-gray-900={unit === 'mi'}
      class:text-white={unit === 'mi'}
      onclick={() => (unit = 'mi')}>
      Miles
    </button>
    <button
      class="px-3 py-1 rounded-md border text-sm"
      class:bg-gray-900={unit === 'km'}
      class:text-white={unit === 'km'}
      onclick={() => (unit = 'km')}>
      Kilometers
    </button>
  </div>

  <!-- Mode Selector -->
  <div class="flex gap-3">
    <button class="px-4 py-2 rounded-md border text-sm transition"
      class:bg-gray-900={mode === 'pace'}
      class:text-white={mode === 'pace'}
      onclick={() => (mode = 'pace')}>
      Calculate Pace
    </button>

    <button class="px-4 py-2 rounded-md border text-sm transition"
      class:bg-gray-900={mode === 'time'}
      class:text-white={mode === 'time'}
      onclick={() => (mode = 'time')}>
      Calculate Time
    </button>

    <button class="px-4 py-2 rounded-md border text-sm transition"
      class:bg-gray-900={mode === 'distance'}
      class:text-white={mode === 'distance'}
      onclick={() => (mode = 'distance')}>
      Calculate Distance
    </button>
  </div>

  <!-- Inputs -->
  <div class="space-y-4">

    {#if mode !== 'distance'}
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1" for="distance">
          Distance ({unit})
        </label>
        <input
          type="number"
          id="distance"
          min="0"
          step="0.01"
          bind:value={distance}
          class="w-full border rounded-md px-3 py-2"
        />
      </div>
    {/if}

    {#if mode !== 'time'}
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1" for="time_min">
          Time
        </label>
        <div class="flex gap-3">
          <input
            type="number"
            id="time_min"
            min="0"
            bind:value={timeMin}
            class="w-24 border rounded-md px-3 py-2"
            placeholder="min"
          />
          <input
            type="number"
            id="time_secs"
            min="0"
            max="59"
            bind:value={timeSec}
            class="w-24 border rounded-md px-3 py-2"
            placeholder="sec"
          />
        </div>
      </div>
    {/if}

    {#if mode !== 'pace'}
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-1" for="pace_min">
          Pace (per {unit})
        </label>
        <div class="flex gap-3">
          <input
            type="number"
            id="pace_min"
            min="0"
            bind:value={paceMin}
            class="w-24 border rounded-md px-3 py-2"
            placeholder="min"
          />
          <input
            type="number"
            id="pace_secs"
            min="0"
            max="59"
            bind:value={paceSec}
            class="w-24 border rounded-md px-3 py-2"
            placeholder="sec"
          />
        </div>
      </div>
    {/if}

  </div>

  <!-- Result -->
  {#if mode === 'pace'}
    <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
      <p class="text-sm text-blue-700 font-medium">Pace (per {unit})</p>
      <p class="text-4xl font-bold text-blue-900 mt-1">
        {result().min}m {result().sec}s
      </p>
    </div>
  {/if}

  {#if mode === 'time'}
    <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
      <p class="text-sm text-blue-700 font-medium">Total Time</p>
      <p class="text-4xl font-bold text-blue-900 mt-1">
        {result().min}m {result().sec}s
      </p>
    </div>
  {/if}

  {#if mode === 'distance'}
    <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
      <p class="text-sm text-blue-700 font-medium">Distance</p>
      <p class="text-4xl font-bold text-blue-900 mt-1">
        {resultDistance()}
      </p>
    </div>
  {/if}

</div>
