<template>
  <div class="route">
    <div class="route__top">
      <p class="route__airport">{{ flight.originCode }}</p>
      <div class="route__range">{{ travelTime }}</div>
      <p class="route__airport">{{ flight.destinationCode }}</p>
    </div>
    <div class="route__divider divider">
      <span class="divider__dot divider__dot--left"></span>
      <span class="divider__dot divider__dot--middle"></span>
      <span class="divider__dot divider__dot--right"></span>
    </div>
    <p v-if="flight.stops" class="route__bottom">через Шымкент, 1 ч 50 м</p>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import { Flight } from "@/entities/Flight";

export default defineComponent({
  name: "RouteInfo",
  props: {
    flight: {
      type: Object as PropType<Flight>,
      required: true,
    },
  },
  setup(props) {
    const travelTime = computed(() => {
      const time = props.flight.travelTime;
      const h = Math.floor(time / 3600);
      const m = Math.floor((time - h * 3600) / 60);

      return `${h} ч ${m} м`;
    });

    return {
      travelTime,
    };
  },
});
</script>

<style lang="scss" scoped>
.route {
  width: 100%;

  &__top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 2px;
    font-size: rem(12);
  }

  &__airport {
    color: $gray-color;
  }

  &__bottom {
    margin-top: 2px;
    font-size: rem(12);
    color: $warn-color;
    text-align: center;
  }
}

.divider {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;

  &:after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    height: 1px;
    background-color: $gray-color;
  }

  &__dot {
    width: 5px;
    height: 5px;
    background-color: white;
    border-radius: 50%;
    border: 1px solid $gray-color;
    z-index: 1;
  }
}
</style>
