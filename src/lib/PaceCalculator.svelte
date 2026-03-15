<script lang="ts">
  // User-controlled state
  let mode = $state<'pace' | 'time' | 'distance'>('pace');

  let distance = $state(1);
  let timeMin = $state(0);
  let timeSec = $state(0);
  let paceMin = $state(0);
  let paceSec = $state(0);

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
    return distance > 0 ? fromMinutes(total / distance) : null;
  };

  const computeTime = () => {
    const pace = toMinutes(paceMin, paceSec);
    return fromMinutes(pace * distance);
  };

  const computeDistance = () => {
    const total = toMinutes(timeMin, timeSec);
    const pace = toMinutes(paceMin, paceSec);
    return pace > 0 ? total / pace : null;
  };

  // Derived values
  let result = $derived(
    mode === "pace"
      ? computePace()
      : mode === "time"
      ? computeTime()
      : computeDistance()
  );

  // Safe distance string (prevents null.toFixed)
  let distance_miles = $derived(() => {
    const d = computeDistance();
    return d !== null ? d.toFixed(2) + " miles" : "—";
  });
</script>

<div class="w-full bg-white shadow-2xl rounded-2xl p-8 space-y-6 border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">Pace Calculator</h1>

  <!-- Mode Selector -->
  <div class="flex gap-3">
    <button
      class="px-4 py-2 rounded-md border text-sm transition"
      class:bg-gray-900={mode === 'pace'}
      class:text-white={mode === 'pace'}
      onclick={() => (mode = 'pace')}>
      Calculate Pace
    </button>

    <button
      class="px-4 py-2 rounded-md border text-sm transition"
      class:bg-gray-900={mode === 'time'}
      class:text-white={mode === 'time'}
      onclick={() => (mode = 'time')}>
      Calculate Time
    </button>

    <button
      class="px-4 py-2 rounded-md border text-sm transition"
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
          Distance (miles)
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
        <label class="block text-sm font-medium text-gray-700 mb-1" for="time">
          Time
        </label>
        <div class="flex gap-3">
          <input
            type="number"
            id="time"
            min="0"
            bind:value={timeMin}
            class="w-24 border rounded-md px-3 py-2"
            placeholder="min"
          />
          <input
            type="number"
            id="time"
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
        <label class="block text-sm font-medium text-gray-700 mb-1" for="pace">
          Pace (per mile)
        </label>
        <div class="flex gap-3">
          <input
            type="number"
            id="pace"
            min="0"
            bind:value={paceMin}
            class="w-24 border rounded-md px-3 py-2"
            placeholder="min"
          />
          <input
            type="number"
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
  {#if mode === 'pace' && result}
    <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
      <p class="text-sm text-blue-700 font-medium">Pace (per mile)</p>
      <p class="text-4xl font-bold text-blue-900 mt-1">
        {result.min}m {result.sec}s
      </p>
    </div>
  {/if}

  {#if mode === 'time' && result}
    <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
      <p class="text-sm text-blue-700 font-medium">Total Time</p>
      <p class="text-4xl font-bold text-blue-900 mt-1">
        {result.min}m {result.sec}s
      </p>
    </div>
  {/if}

  {#if mode === 'distance'}
    <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 text-center shadow-inner">
      <p class="text-sm text-blue-700 font-medium">Distance</p>
      <p class="text-4xl font-bold text-blue-900 mt-1">
        {distance_miles()}
      </p>
    </div>
  {/if}

</div>
