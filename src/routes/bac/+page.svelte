<script>
  import BAC from "$lib/BAC.svelte";
</script>

<section class="space-y-4 mb-8">
  <h1 class="text-3xl font-bold text-gray-900">BAC Calculator</h1>

  <p class="text-gray-700 leading-relaxed">
    This calculator provides an estimate of your blood alcohol concentration
    (BAC) based on your weight, number of drinks, time since drinking began,
    and gender. It’s intended for general awareness and educational purposes.
  </p>

  <p class="text-gray-700 leading-relaxed">
    Many factors influence actual BAC, including metabolism, food intake, and
    individual tolerance. Because of this, the results should never be used to
    determine whether it is safe to drive or operate machinery.
  </p>

  <p class="text-gray-700 leading-relaxed">
    When in doubt, always choose a safe alternative to driving.
  </p>
</section>

<BAC />
