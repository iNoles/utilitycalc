<script lang="ts">
  // State
  let amount = 0;
  let tipPercent = 0.15;
  let split = 1;
  let tipPercentInput = 15;

  const presetTips = [0.10, 0.15, 0.18, 0.20, 0.25];

  // Calculations (classic Svelte reactivity)
  $: tipAmount = amount * tipPercent;
  $: totalAmount = amount + tipAmount;
  $: tipPerPerson = tipAmount / split;
  $: totalPerPerson = totalAmount / split;

  const fmt = (v: number) => v.toFixed(2)

  function updateTipPercent() {
    tipPercent = tipPercentInput / 100;
  }
</script>

<div class="space-y-6 p-6 bg-white rounded-2xl shadow-xl border border-gray-200">

  <h1 class="text-2xl font-semibold text-gray-800 text-center">Tip Calculator</h1>

  <!-- Bill -->
  <div>
    <label class="block text-sm font-medium mb-1" for="bill_total">Bill Total ($)</label>
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
    <label class="block text-sm font-medium mb-2" for="tip_perc">Tip Percentage</label>

    <!-- Preset Tip Buttons -->
    <div class="flex gap-2 mt-1 overflow-x-auto pb-1">
      {#each presetTips as p}
        <button
          id="tip_perc"
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
      <label class="text-sm font-medium w-20" for="custom_tip">Custom:</label>

      <input
        id="custom_tip"
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
    <label class="block text-sm font-medium mb-1" for="split">Split Between</label>

    <div class="flex items-center justify-center gap-3 mt-2">
      <!-- Minus -->
      <button
        class="w-10 h-10 flex items-center justify-center border rounded-full text-xl font-medium transition active:scale-[0.97]"
        onclick={() => split = Math.max(1, split - 1)}>
        –
      </button>

      <!-- Input -->
      <div class="w-16 h-10 flex items-center justify-center border rounded-full">
        <input
          id="split"
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

      <div>
        <p class="text-sm text-blue-700 font-medium">Tip Total</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(tipAmount)}
        </p>
      </div>

      <div>
        <p class="text-sm text-blue-700 font-medium">Bill + Tip</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(totalAmount)}
        </p>
      </div>

      <div>
        <p class="text-sm text-blue-700 font-medium">Tip / Person</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(tipPerPerson)}
        </p>
      </div>

      <div>
        <p class="text-sm text-blue-700 font-medium">Each Person Pays</p>
        <p class="text-2xl font-bold text-blue-900">
          ${fmt(totalPerPerson)}
        </p>
      </div>

    </div>
  </div>

</div>
