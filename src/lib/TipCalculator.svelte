<script lang="ts">
  // State
  let amount = 0;
  let tipPercent = 0.15;
  let split = 1;
  let tipPercentInput = 15;

  const presetTips = [0.10, 0.15, 0.18, 0.20, 0.25];

  // Rounding modes (only one active at a time)
  let roundTips = false;
  let roundTotals = false;

  // Round to nearest whole dollar (restaurant style)
  function roundToDollar(v: number) {
    return Math.round(v);
  }

  // Raw calculations
  $: tipAmountRaw = amount * tipPercent;
  $: totalAmountRaw = amount + tipAmountRaw;

  $: tipPerPersonRaw = tipAmountRaw / split;
  $: totalPerPersonRaw = totalAmountRaw / split;

  // Apply rounding
  $: tipAmount = roundTips ? roundToDollar(tipAmountRaw) : tipAmountRaw;
  $: tipPerPerson = roundTips ? roundToDollar(tipPerPersonRaw) : tipPerPersonRaw;

  $: totalAmount = roundTotals ? roundToDollar(totalAmountRaw) : totalAmountRaw;
  $: totalPerPerson = roundTotals ? roundToDollar(totalPerPersonRaw) : totalPerPersonRaw;

  // Formatting
  const fmt = (v: number) => v.toFixed(2);

  function updateTipPercent() {
    tipPercent = tipPercentInput / 100;
  }
</script>

<div class="space-y-6 p-6 bg-white rounded-2xl shadow-xl border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">Tip Calculator</h1>

  <!-- Bill -->
  <div>
    <label for="bill_total" class="block text-sm font-medium mb-1">Bill Total ($)</label>
    <input
      id="bill_total"
      type="number"
      bind:value={amount}
      min="0"
      step="0.01"
      inputmode="decimal"
      class="w-full border rounded-lg px-3 py-2 text-center"
    />
  </div>

  <!-- Tip -->
  <div>
    <label for="tip_percent_input" class="block text-sm font-medium mb-2">Tip Percentage</label>

    <!-- Preset Tip Buttons -->
    <div class="flex gap-2 mt-1 overflow-x-auto pb-1">
      {#each presetTips as p}
        <button
          class="px-4 py-2 rounded-full border text-sm font-medium whitespace-nowrap flex-shrink-0 transition hover:bg-gray-100 active:scale-[0.97]"
          class:bg-blue-600={tipPercent === p}
          class:text-white={tipPercent === p}
          class:border-blue-600={tipPercent === p}
          onclick={() => {
            tipPercent = p;
            tipPercentInput = Math.round(p * 100);
          }}
        >
          {Math.round(p * 100)}%
        </button>
      {/each}
    </div>

    <!-- Custom Tip -->
    <div class="flex items-center gap-3 mt-3">
      <label for="tip_percent_input" class="text-sm font-medium w-20">Custom:</label>
      <input
        id="tip_percent_input"
        type="number"
        min="0"
        max="100"
        bind:value={tipPercentInput}
        oninput={updateTipPercent}
        class="w-24 px-4 py-2 border border-gray-300 rounded-full text-center text-sm font-medium"
      />
      <span class="text-gray-700 text-sm font-medium">%</span>
    </div>
  </div>

  <!-- Split -->
  <div>
    <label for="split" class="block text-sm font-medium mb-1">Split Between</label>

    <div class="flex items-center justify-center gap-3 mt-2">
      <button
        class="w-10 h-10 flex items-center justify-center border rounded-full text-xl font-medium transition active:scale-[0.97]"
        onclick={() => split = Math.max(1, split - 1)}
      >
        –
      </button>

      <div class="w-16 h-10 flex items-center justify-center border rounded-full">
        <input
          id="split"
          type="number"
          min="1"
          bind:value={split}
          class="w-full text-center text-lg font-semibold outline-none bg-transparent"
        />
      </div>

      <button
        class="w-10 h-10 flex items-center justify-center border rounded-full text-xl font-medium transition active:scale-[0.97]"
        onclick={() => split++}
      >
        +
      </button>
    </div>
  </div>

  <!-- Rounding Options -->
  <div class="mt-6 space-y-3">
    <p id="rounding_label" class="block text-sm font-medium">Rounding</p>

    <div aria-labelledby="rounding_label" class="flex gap-3 flex-wrap">
      <button
        class="px-4 py-2 rounded-full border text-sm font-medium transition hover:bg-gray-100"
        class:bg-blue-600={roundTips}
        class:text-white={roundTips}
        onclick={() => {
          roundTips = !roundTips;
          if (roundTips) roundTotals = false;
        }}
      >
        Round Tip
      </button>

      <button
        class="px-4 py-2 rounded-full border text-sm font-medium transition hover:bg-gray-100"
        class:bg-blue-600={roundTotals}
        class:text-white={roundTotals}
        onclick={() => {
          roundTotals = !roundTotals;
          if (roundTotals) roundTips = false;
        }}
      >
        Round Total
      </button>
    </div>
  </div>

  <!-- Results -->
  <div class="bg-blue-50 border border-blue-200 rounded-xl p-6 shadow-inner">
    <div class="grid grid-cols-2 gap-6">
      <div>
        <p class="text-sm text-blue-700 font-medium">Tip Total</p>
        <p class="text-2xl font-bold text-blue-900">${fmt(tipAmount)}</p>
      </div>

      <div>
        <p class="text-sm text-blue-700 font-medium">Bill + Tip</p>
        <p class="text-2xl font-bold text-blue-900">${fmt(totalAmount)}</p>
      </div>

      <div>
        <p class="text-sm text-blue-700 font-medium">Tip / Person</p>
        <p class="text-2xl font-bold text-blue-900">${fmt(tipPerPerson)}</p>
      </div>

      <div>
        <p class="text-sm text-blue-700 font-medium">Each Person Pays</p>
        <p class="text-2xl font-bold text-blue-900">${fmt(totalPerPerson)}</p>
      </div>
    </div>
  </div>
</div>
