<script lang="ts">
  import { expected_from_config } from "./calcs";
  import type { Result } from "./calcs";
  import type { Config } from "./types";

  export let config: Config;

  const round_to = (num: number, precision: number) => {
    const factor = 10 ** precision;
    return Math.round(num * factor) / factor;
  };

  const display_cost = (num: number) => {
    if (Number.isNaN(num)) {
      return "";
    }

    const nf = Intl.NumberFormat();
    if (num < 1_000_000_000) {
      return `${nf.format(round_to(num / 1e6, 2))}m`;
    } else if (num < 1_000_000_000_000) {
      return `${nf.format(round_to(num / 1e9, 2))}b`;
    } else {
      return `${nf.format(round_to(num / 1e12, 2))}t`;
    }
  };

  const display_two_decimals = (num: number) => {
    if (Number.isNaN(num)) {
      return "";
    }

    return round_to(num, 2);
  };

  let result: Result;
  $: result = expected_from_config(config);
</script>

<output>
  <div class="header">
    <div class="summary mesos">
      <div class="description">Mesos</div>
      <div class="value">
        {display_cost(result.cost)}
      </div>
    </div>
    <div class="summary prob-make">
      <div class="description">% success before boom</div>
      <div class="value">
        {display_two_decimals(100 * result.prob_success)}%
      </div>
    </div>
    <div class="summary booms">
      <div class="description">Booms</div>
      <div class="value">
        {display_two_decimals(result.booms)}
      </div>
    </div>
  </div>
</output>

<style lang="postcss">
  @tailwind utilities;

  .header {
    @apply flex justify-between;
    @apply my-12;
    @apply flex-wrap gap-y-8;

    .summary {
      .description {
        font-weight: 500;
        @apply text-2xl;
      }

      .value {
        @apply text-7xl;
      }

      &.mesos {
        @apply text-amber-400;
        text-align: left;
      }

      &.prob-make {
        @apply text-gray-400;
        text-align: center;

        @apply order-3 basis-full;
        @apply md:order-none md:basis-auto;
      }

      &.booms {
        @apply text-red-600;
        text-align: right;
      }
    }
  }
</style>
