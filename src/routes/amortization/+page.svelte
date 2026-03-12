<script>
  import Amortization from "$lib/Amortization.svelte";
</script>

<section class="space-y-4 mb-8">
  <h1 class="text-3xl font-bold text-gray-900">Loan Amortization Calculator</h1>

  <p class="text-gray-700 leading-relaxed">
    This calculator estimates your monthly loan payment based on the loan
    amount, interest rate, and term. It also shows the total amount paid over
    the life of the loan and how much of that total is interest.
  </p>

  <p class="text-gray-700 leading-relaxed">
    These insights help you compare loan offers, understand the long‑term cost
    of borrowing, and evaluate whether refinancing or choosing a shorter term
    could reduce your overall interest.
  </p>

  <p class="text-gray-700 leading-relaxed">
    It’s a practical way to break down the financial impact of major purchases
    like vehicles, home improvements, or consolidating debt.
  </p>
</section>

<Amortization />
