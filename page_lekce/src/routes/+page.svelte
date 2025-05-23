<h1>Welcome to your library project</h1>
<p>Create your package using @sveltejs/package and preview/showcase your work with SvelteKit</p>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<script>
    let dostupnaLekce = 1;
  </script>
  
  <h1 style="margin-bottom: 75px">Kalendář tvých lekcí</h1>
  
  <div style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 7px;">
    {#each Array(10) as _, i}
      <div style="
        margin: 10px;
        width: 100px;
        height: 80px;
        border: 2px solid #ccc;
        padding: 10px;
        text-align: center;
        border-radius: 10px;
        background: {i + 1 === dostupnaLekce ? '#000' : 'white'};
        color: {i + 1 === dostupnaLekce ? 'white' : 'black'};
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 4px;
      ">
        <div style="font-weight: bold;">Lekce {i + 1}</div>
  
        {#if i + 1 === dostupnaLekce}
          <div style="
            background-color: white;
            color: black;
            padding: 1px 2px 1px ;
            border-radius: 4px;
            font-size: 12px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
          ">
            <strong>dostupná lekce</strong>
          </div>
        {/if}
      </div>
    {/each}
  </div>