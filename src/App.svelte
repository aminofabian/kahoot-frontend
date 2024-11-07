<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'



  async function getQuizzes(){
let response = await fetch("http://localhost:3000/api/quizes")
if(!response.ok){
  throw new Error("Failed to fetch quizzes");
  return;
}
let json = await response.json();
console.log(json);
}

function connect(){
let websocket = new WebSocket("ws://localhost:3000/ws");

websocket.onopen = () => {
  console.log("Connected to websocket");

  websocket.send("Hello from client");
};

websocket.onmessage = (event) => {
  console.log("Received message from websocket", event.data);
};

}

</script>

<button on:click={getQuizzes}>Get Quizzes</button>
<button on:click={connect}>Connect</button>

<main>
  <div>
    <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
