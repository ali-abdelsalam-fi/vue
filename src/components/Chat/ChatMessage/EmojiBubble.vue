<script setup>
// A chat bubble container
import useIcons from "../../../compositionFunctions/useIcons";
import useChatBubblePosition from "../useChatBubblePosition";

const props = defineProps({
  direction: {
    type: String,
    default: "right",
  },
  emoji:{
    type: String,
  },
});

const icons = useIcons();

console.log(`props.emoji is ${props.emoji}`)
// Import CSS variables from a 'hook'
const { cssVars } = useChatBubblePosition(props.direction);
</script>

<template>
  <img :src="icons[props.emoji]" :alt="props.emoji" :style="cssVars" />
</template>

<style scoped lang="scss">
img {
  width: 40px;
  height: 40px;
  display: inline-block;
  position: relative;
  align-self: var(--align);
  margin: var(--margin);
}

</style>
