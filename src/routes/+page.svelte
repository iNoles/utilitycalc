<script>
  const calculators = [
    { name: "Gas Mileage Calculator", path: "gas-mileage", desc: "Calculate miles per gallon based on miles driven and fuel used." },
    { name: "Loan Amortization Calculator", path: "amortization", desc: "Estimate monthly payments, total cost, and interest paid." },
    { name: "BAC Calculator", path: "bac", desc: "Estimate blood alcohol concentration based on drinks, weight, and time." },
    { name: "Fuel Savings Comparison", path: "fuel-comparison", desc: "Compare yearly fuel costs between two vehicles." }
  ];

</script>

<div class="space-y-12">

  <!-- Hero Section -->
  <section class="text-center space-y-3">
    <h1 class="text-4xl font-bold text-gray-900">UtilityCalc</h1>
    <p class="text-gray-600 text-lg">
      Simple, accurate calculators for everyday decisions.
    </p>
  </section>

  <!-- Calculator Grid -->
  <section>
    <div class="grid gap-6 sm:grid-cols-2">
      {#each calculators as calc}
        <a
          href={calc.path}
          class="block bg-white p-6 rounded-2xl shadow-md border border-gray-200 hover:shadow-xl hover:-translate-y-1 transition-all"
        >
          <h2 class="text-xl font-semibold text-gray-800 mb-2">{calc.name}</h2>
          <p class="text-gray-600 text-sm leading-relaxed">{calc.desc}</p>
        </a>
      {/each}
    </div>
  </section>

</div>
