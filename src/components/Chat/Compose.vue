<script setup>
import { ref } from "vue";
import Input from "../generic/form/Input.vue";
import Button from "../generic/form/Button.vue";

// Store the text input value. This is a reactive 'state' variable.
const text = ref("");

/**
 * Handle changes to the text input value
 * @param {String} newValue New text value
 */
const onChange = (newValue) => {
  text.value = newValue;

};

// Components emit events. Parent components listen to these events. Just like the DOM!
const emit = defineEmits(["send"]);

/**
 * Sends a text message.
 */
function send(type) {
  // Hint: Call 'emit' with the correct arguments.
  //       Finally, clear the text input.
  console.log(text.value);
  if(text.value){
    emit("send",text.value, type)  // Hint: You can provide more parameters to 'emit'.
  }
  text.value="";
}

</script>

<template>
  <div class="compose">
    <!-- An emoji selector could go here, for example. The choice is yours! -->
    <div class="emoji-selector">
      <Button icon="shrug" @click="onChange('shrug');send('emoji');" />
      <Button icon="octopus" @click="onChange('octopus');send('emoji')" />
      <Button icon="mushroom" @click="onChange('mushroom');send('emoji')" />
      <Button icon="fire" @click="onChange('fire');send('emoji')" />
      <Button icon="tent" @click="onChange('tent');send('emoji')" />
    </div>
    <div class="message-row">
      <Input
        :value="text"
        placeholder="Type a message"
        @change="onChange"
        @keydown.enter="send('text')"
      />
      <Button icon="send" @click="send('text')" />
    </div>
  </div>
</template>

<style scoped>
.message-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.5rem;
}
/* This targets a nested component with scoped styles*/
.compose:deep(.emoji-selector) {
  margin-bottom: 0.5rem;
}
</style>
