<script>
  let principal = $state(0);
  let rate = $state(0);
  let years = $state(0);

  let monthlyRate = $derived(rate > 0 ? rate / 100 / 12 : 0);
  let months = $derived(years * 12);

  let monthlyPayment = $derived(
    principal > 0 && rate > 0 && years > 0
      ? (
          (principal * monthlyRate) /
          (1 - Math.pow(1 + monthlyRate, -months))
        ).toFixed(2)
      : "—"
  );

  let totalPaid = $derived(
    monthlyPayment !== "—" ? (monthlyPayment * months).toFixed(2) : "—"
  );

  let totalInterest = $derived(
    totalPaid !== "—" ? (totalPaid - principal).toFixed(2) : "—"
  );
</script>

<div class="w-full bg-white shadow-2xl rounded-2xl p-8 space-y-6 border border-gray-200">
  <h1 class="text-2xl font-semibold text-gray-800 text-center">Loan Amortization Calculator</h1>

  <div class="space-y-4">
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="loan-amount">Loan Amount</label>
      <input
        type="number"
        id="loan-amount"
        bind:value={principal}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-green-500 focus:outline-none"
        placeholder="Enter amount"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="interest-rate">Interest Rate (%)</label>
      <input
        type="number"
        id="interest-rate"
        bind:value={rate}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-green-500 focus:outline-none"
        placeholder="Annual rate"
      />
    </div>

    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1" for="loan-term">Loan Term (Years)</label>
      <input
        type="number"
        id="loan-term"
        bind:value={years}
        class="w-full px-4 py-2 rounded-lg border border-gray-300 focus:ring-2 focus:ring-green-500 focus:outline-none"
        placeholder="Years"
      />
    </div>
  </div>

  <div class="bg-green-50 border border-green-200 rounded-xl p-6 shadow-inner space-y-2">
    <div class="text-center">
      <p class="text-sm text-green-700 font-medium">Monthly Payment</p>
      <p class="text-3xl font-bold text-green-900">{monthlyPayment}</p>
    </div>

    <div class="flex justify-between text-sm text-gray-700 pt-4">
      <span>Total Paid:</span>
      <span class="font-semibold">${totalPaid}</span>
    </div>

    <div class="flex justify-between text-sm text-gray-700">
      <span>Total Interest:</span>
      <span class="font-semibold">${totalInterest}</span>
    </div>
  </div>
</div>
