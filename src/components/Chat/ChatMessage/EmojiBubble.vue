<script setup>
// A chat bubble container
import useChatBubblePosition from "../useChatBubblePosition";

const props = defineProps({
  direction: {
    type: String,
    default: "right",
  },
});

// Import CSS variables from a 'hook'
const { cssVars } = useChatBubblePosition(props.direction);
</script>

<template>
  <div :style="cssVars">
    <slot />
  </div>
</template>

<style scoped lang="scss">
img {
  width: 48px;
  height: 48px;
  display: inline-block;
  position: relative;
  align-self: var(--align);
  margin: var(--margin);
}

</style>
