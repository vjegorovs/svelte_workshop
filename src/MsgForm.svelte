<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  let text = "test1234v";
  let disableFormSending = false;
  $: disableFormSending = text.length > 4;

  const sendMessage = () => {
    dispatch("send", { text });
  };
</script>

<input bind:value={text} />
<button on:click={sendMessage} disabled={!disableFormSending}>Send</button>
{text}
