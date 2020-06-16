<script>
  import MsgForm from "./MsgForm.svelte";
  import MsgList from "./MsgList.svelte";
  import { onMount } from "svelte";
  import { testWebSocket } from "./ws";
  export let name;
  let websocket;

  const sendMessage = ({ detail }) => {
    websocket.send(detail.text);
    console.log("Sending message: ", detail.text);
  };

  let messages = [];

  onMount(() => {
    websocket = testWebSocket();
    websocket.onmessage = ({ data }) => {
      console.log("Received message: ", data);
      messages = [...messages, data];
    };
  });
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <header>Svelte Chat</header>
  <MsgList {messages} />
  <MsgForm on:send={sendMessage} />
</main>
