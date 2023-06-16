<script lang="ts" setup>
import Popper from "vue3-popper";
export type Placement =
  | "auto"
  | "auto-start"
  | "auto-end"
  | "top"
  | "top-start"
  | "top-end"
  | "bottom"
  | "bottom-start"
  | "bottom-end"
  | "right"
  | "right-start"
  | "right-end"
  | "left"
  | "left-start"
  | "left-end";

///// https://valgeirb.github.io/vue3-popper/guide/api.html#props

const props = withDefaults(
  defineProps<{
    placement?: Placement;
    arrow?: boolean;
    hover?: boolean;
    disableClickAway?: boolean;
    interactive?: boolean;
    show?: boolean;
    zIndex?: number;
    locked?: boolean;
    offsetDistance?: number;
  }>(),
  {
    placement: "right",
    arrow: false,
    hover: false,
    disableClickAway: false,
    interactive: true,
    show: undefined,
    zIndex: 9999,
    locked: false,
    offsetDistance: 12,
  }
);
</script>

<template>
  <Popper
    v-bind="$attrs"
    :placement="placement"
    :arrow="arrow"
    :hover="hover"
    :disable-click-away="disableClickAway"
    :interactive="interactive"
    :show="show"
    :z-index="zIndex"
    :locked="locked"
    class="popper-wrapper"
  >
    <slot />
    <template #content="props">
      <slot name="content" v-bind="props" />
    </template>
  </Popper>
</template>

<style lang="scss" scoped>
.popper-wrapper {
  --popper-theme-background-color: #ffffff;
  --popper-theme-background-color-hover: #ffffff;
  --popper-theme-border-radius: 0.5rem;
  --popper-theme-padding: 0;
  --popper-theme-box-shadow: 0 6px 30px -6px rgba(0, 0, 0, 0.25);
}
</style>
