<script lang="ts">
  import TipCalculator from "$lib/TipCalculator.svelte";
</script>

<section class="space-y-4 mb-8">
  <h1 class="text-3xl font-bold text-gray-900">Tip Calculator</h1>

  <p class="text-gray-700 leading-relaxed">
    This calculator helps you quickly determine the right tip amount based on
    your bill total and preferred tip percentage. You can choose from common
    preset percentages or enter a custom amount for full control.
  </p>

  <p class="text-gray-700 leading-relaxed">
    It also supports splitting the bill between multiple people, showing both
    the total tip and the per‑person share. This makes it easy to settle group
    meals, nights out, or shared expenses without any mental math.
  </p>

  <p class="text-gray-700 leading-relaxed">
    Whether you're dining out, ordering delivery, or sharing costs with
    friends, this tool gives you a fast, accurate breakdown of what everyone
    owes.
  </p>
</section>

<TipCalculator />
