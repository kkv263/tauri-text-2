<script lang='ts'>
  import { invoke } from '@tauri-apps/api/tauri';
  import { WebviewWindow } from '@tauri-apps/api/window';
  import { fade } from 'svelte/transition';

  // const webview = new WebviewWindow('theUniqueLabael', {
  //   url: '/text',
  // })

  // webview.once('tauri://created', function () {
  // // webview window successfully created
  //   console.log('created');
  // })
  // webview.once('tauri://error', function (e) {
  //   // an error happened creating the webview window
  //   console.log('error',e);
  // })
  
  let messages:any[] = [];
  let message = '';
  let greetMsg = '';

  async function greet(){
    if (message === '') return;
    // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
    // greetMsg = await invoke('greet', { message })
    messages.splice(0, 0, message);
    message = '';

    if (messages.length > 3) { messages.pop(); }

    messages = messages;
  }
</script>

<form on:submit|preventDefault={greet}>
  <div class="bubble-container">
    {#each messages as msg}
      <p transition:fade class='bubble'>{msg}</p>
    {/each}
  </div>
  <div class='row'>
    <input id='greet-input' placeholder='Enter a message' bind:value={message} />
    <button type='submit'>
      <svg width='24px' height='24px' xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" d="M12.75 15l3-3m0 0l-3-3m3 3h-7.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
    </button>
  </div>
</form>

<style lang="scss">
  .row  {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    display: flex;
    input {
      flex: 1 0 auto;
      padding: 8px;
      font-size: 16px;
      background-color: #272A2F;
      margin: 0;
      color: #fff;
    }

    button {
      color: #fff;
      background-color: #C440DA;
      font-size: 16px;
      padding: 8px 16px;
      border: 0;
      margin: 0;
      cursor: pointer;
      transition: all .2s ease;
      display: flex;
      align-items: center;
      justify-content: center;

      &:hover {
        background-color: darken(#C440DA, 10%);
      }
    }
  }

  .bubble-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .bubble {
    background-color: #fff;
    color: #000;
    padding: 8px 16px;
    border-radius: 8px;
    width: 200px;
    text-align: left;
  }
</style>