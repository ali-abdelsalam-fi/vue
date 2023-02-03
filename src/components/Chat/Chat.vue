<script setup>
// Main chat component
import { provide, ref } from "vue";
import CenterOnPage from "../generic/containers/CenterOnPage.vue";
import ChatMessage from "./ChatMessage/ChatMessage.vue";
import Compose from "./Compose.vue";
import useAutoScrollToBottom from "../../compositionFunctions/useAutoScrollToBottom";
import existingMessages from "./messages";

// The active user's id.
const USER_ID = 1111;

// Create a reactive variable from existing messages. Similar to useState.
const messages = ref(existingMessages);

// Use a behavior that automatically scrolls the message list to the bottom whenever its content changes.
const messageListElement = ref(null); // Create a ref that we attach to a DOM element. Similar to useRef.
useAutoScrollToBottom(messageListElement); // Using a "hook".

// Provide the active user's id to all components in this tree. Similar to providing a React Context.
provide("userId", USER_ID);



function updateChat(newText){
  console.log(newText);
  // var currentDate = new Date().toISOString().toString();
  // console.log(currentDate);
  // console.log(currentDatedate.toLocaleTimeString("fi-FI", {hour: "2-digit",minute: "2-digit",}););
  let newMessage = {  
    content: newText,
    type: "text",
    senderId: USER_ID,
    timestamp: new Date()}
    // timestamp: new Date(currentDate)}
    // timestamp: new Date("2022-01-26T11:37:42.947Z")}
    // timestamp: new Date("2023-02-02T21:08:44.264Z")}
    // timestamp: currentDate}    
  //  messages.value = [...messages.value, messages.value[0]]
  messages.value = [...messages.value, newMessage]
};

</script>

<template>
  <CenterOnPage>
    <div class="chat shadow-2">
      <div ref="messageListElement" class="message-list">
        <!-- Iterate over elements with v-for -->
        <ChatMessage
          v-for="message in messages"
          :key="`${message.senderId}:${message.timestamp}`"
          :message="message"
        />
      </div>

      <!-- Hint: Create a function that adds new messages to 'messages'.
                 Make the <Compose /> component call this function whenever a 'send' event is emitted.

           Tip:  In your function, you can replace 'messages.value' directly ie. 'messages.value = [...messages.value, newMessage]'
      -->
      <!--
              @send="i => updateChat(i)" 
      -->           
      <Compose
      @send="text => updateChat(text)" 
      
      />
    </div>
  </CenterOnPage>
</template>

<style scoped lang="scss">
.chat {
  width: 100%;
  max-width: 500px;
  min-height: 50vh;
  max-height: 600px;
  margin: 3rem 1rem;
  padding: 2rem;
  border-radius: 7px;
  background: radial-gradient(
      ellipse farthest-side at 76% 77%,
      rgba(245, 228, 212, 0.25) 4%,
      rgba(255, 255, 255, 0) calc(4% + 1px)
    ),
    radial-gradient(circle at 76% 40%, #fef6ec 4%, rgba(255, 255, 255, 0) 4.18%),
    linear-gradient(135deg, #ff0000 0%, #000036 100%),
    radial-gradient(ellipse at 28% 0%, #ffcfac 0%, rgba(98, 149, 144, 0.5) 100%),
    linear-gradient(180deg, #cd6e8a 0%, #f5eab0 69%, #d6c8a2 70%, #a2758d 100%);
  background-blend-mode: normal, normal, screen, overlay, normal;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 1rem;

  .message-list {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    gap: 1rem;
    overflow-y: auto;
    overflow-x: hidden;
    padding-bottom: 0.5rem;
  }
}
</style>
