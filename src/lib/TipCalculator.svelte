<script lang="ts">
  // State
  let bill = $state("0.00");
  let tipPercent = $state(0.15); // default 15%
  let customTip = $state("18");
  let split = $state(1);

  const presetTips = [0.10, 0.15, 0.18, 0.20, 0.25];

  // Safe number parser
  const num = (v: any) => {
    const n = Number(v);
    return isNaN(n) ? 0 : n;
  };

  // Safe formatter for UI
  const fmt = (v: any) => {
    const n = Number(v);
    return isNaN(n) ? "0.00" : n.toFixed(2);
  };

  // Active tip: custom overrides preset
  const activeTip = $derived(() => {
    const c = num(customTip);
    return c > 0 ? c / 100 : tipPercent;
  });

  // Calculations (all NaN‑proof)
  const tipAmount = $derived(() => num(bill) * activeTip);
  const totalAmount = $derived(() => num(bill) + tipAmount);
  const tipPerPerson = $derived(() => num(tipAmount) / split);
  const totalPerPerson = $derived(() => num(totalAmount) / split);
</script>

<div class="space-y-6 p-6 bg-white rounded-2xl shadow-xl border border-gray-200">

  <h1 class="text-2xl font-semibold text-gray-800 text-center">Tip Calculator</h1>

  <!-- Bill -->
  <div>
    <label class="block text-sm font-medium mb-1">Bill Total ($)</label>
    <input
      type="number"
      min="0"
      step="0.01"
      bind:value={bill}
      class="w-full border rounded-lg px-3 py-2 text-center"
    />
  </div>

  <!-- Tip -->
  <div>
    <label class="block text-sm font-medium mb-2">Tip Percentage</label>

    <!-- Pill Buttons -->
    <div class="flex gap-2 mt-1 overflow-x-auto pb-1">
      {#each presetTips as p}
        <button
          class="px-4 py-2 rounded-full border text-sm font-medium whitespace-nowrap flex-shrink-0 transition
                 bg-white text-gray-800 border-gray-300
                 hover:bg-gray-100 active:scale-[0.97]"
          class:bg-gray-900={activeTip === p}
          class:text-white={activeTip === p}
          class:border-gray-900={activeTip === p}
          onclick={() => { tipPercent = p; customTip = ""; }}>
          {Math.round(p * 100)}%
        </button>
      {/each}
    </div>

    <!-- Custom Tip Row -->
    <div class="flex items-center gap-3 mt-3">
      <label class="text-sm font-medium w-20">Custom:</label>

      <input
        type="number"
        min="0"
        max="100"
        bind:value={customTip}
        class="w-24 px-4 py-2 border border-gray-300 rounded-full text-center text-sm font-medium"
      />

      <span class="text-gray-700 text-sm font-medium">%</span>
    </div>
  </div>

  <!-- Split -->
  <div>
    <label class="block text-sm font-medium mb-1">Split Between</label>

    <div class="flex items-center justify-center gap-3 mt-2">

      <!-- Minus -->
      <button
        class="w-10 h-10 flex items-center justify-center border rounded-full text-xl font-medium transition active:scale-[0.97]"
        onclick={() => split = Math.max(1, split - 1)}>
        –
      </button>

      <!-- Textbox wrapper -->
      <div class="w-16 h-10 flex items-center justify-center border rounded-full">
        <input
          type="number"
          min="1"
          bind:value={split}
          class="w-full text-center text-lg font-semibold outline-none bg-transparent"
        />
      </div>

      <!-- Plus -->
      <button
        class="w-10 h-10 flex items-center justify-center border rounded-full text-xl font-medium transition active:scale-[0.97]"
        onclick={() => split++}>
        +
      </button>

    </div>
  </div>

  <!-- Results -->
  <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 shadow-inner">
    <div class="grid grid-cols-2 gap-6">

      <!-- Tip Total -->
      <div>
        <p class="text-sm text-blue-700 font-medium">Tip Total</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(tipAmount)}
        </p>
      </div>

      <!-- Bill + Tip -->
      <div>
        <p class="text-sm text-blue-700 font-medium">Bill + Tip</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(totalAmount)}
        </p>
      </div>

      <!-- Tip Per Person -->
      <div>
        <p class="text-sm text-blue-700 font-medium">Tip / Person</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(tipPerPerson)}
        </p>
      </div>

      <!-- Each Person Pays -->
      <div>
        <p class="text-sm text-blue-700 font-medium">Each Person Pays</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(totalPerPerson)}
        </p>
      </div>

    </div>
  </div>

</div>
