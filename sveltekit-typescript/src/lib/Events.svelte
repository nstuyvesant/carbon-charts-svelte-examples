<script lang="ts">
  import { onMount } from "svelte";
  import { BarChartSimple } from "@carbon/charts-svelte";
  import type { SimpleBarChart } from "@carbon/charts";
  import type { BarChartOptions, ScaleTypes } from "@carbon/charts/interfaces";

  let chart: null | SimpleBarChart = null;

  const options: BarChartOptions = {
    title: "Simple bar (discrete)",
    height: "400px",
    axes: {
      left: { mapsTo: "value" },
      bottom: { mapsTo: "group", scaleType: "labels" as ScaleTypes.LABELS },
    },
  };

  function barMouseOver(e: MouseEvent) {
    console.log(e.detail);
  }

  onMount(() => {
    return () => {
      if (chart) chart.services.events.removeEventListener("bar-mouseover", barMouseOver);
    };
  });

  $: if (chart) chart.services.events.addEventListener("bar-mouseover", barMouseOver);
</script>

<BarChartSimple
  bind:chart
  data={[
    { group: "Qty", value: 65000 },
    { group: "More", value: 29123 },
    { group: "Sold", value: 35213 },
    { group: "Restocking", value: 51213 },
    { group: "Misc", value: 16932 },
  ]}
  {options}
/>
