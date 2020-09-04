<style>
	main{background-color: black;
			width: 100%;
			height: 100%;}
	.Titulo{color: white;
			text-align: center;
			font-size: 30px;
			margin-bottom: 20px;}
	.Listo{color: white;
			text-align: center;
			font-size: 20px;
			margin-top: 20px;}
	.Gris{background-color: white;}
	.Contenedor{max-width: 400px;
				margin: 0 auto;}
	.Item{color: black;
			font-size: 17px;}
	.Final{margin: 0 auto;
			}
	.Copy{color: white;
			text-align: center;}
</style>


<script>
  import { slide } from "svelte/transition";
  import { elasticInOut } from "svelte/easing";

  let todos = [];
  let input = "";

  function addTodo() {
    if (input)
      todos = [
        ...todos,
        {
          text: input,
          id: Math.random()
            .toString(36)
            .substr(2, 9)
        }
      ];
    input = "";
  }

  function removeTodo(id) {
    const index = todos.findIndex(todo => todo.id === id);
    todos.splice(index, 1);
    todos = todos;
  }
</script>

<svelte:head>
  <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/bulma@0.8.0/css/bulma.min.css"/>
  <script src="https://use.fontawesome.com/releases/v5.3.1/js/all.js"></script>
</svelte:head>

<main class="container is-fluid">
  <div class="columns is-centered is-vcentered is-mobile">
    <div class="column is-narrow" style="width: 70%">
    <br>
      <h1 class="Titulo">TO-DO LIST</h1>
      <form class="field has-addons" style="justify-content: center" on:submit|preventDefault={addTodo}>
        <div class="control">
          <input bind:value={input} class="input" type="text" placeholder="Next Task">
        </div>
        <div class="control">
          <button class="button is-info">
            <span class="icon is-small">
              <i class="fas fa-plus"></i>
            </span>
          </button>
        </div>
      </form>
      <div class="Contenedor">
      <ul class:list={todos.length > 0}>
        {#each todos as todo (todo.id)}
          <li class="Gris list-item" transition:slide="{{duration: 300, easing: elasticInOut}}">
            <div class="is-flex" style="align-items: center">
              <span class="Item">{todo.text}</span>
              <div style="flex: 1"></div>
              <button class="button is-danger is-outlined is-small" on:click={()=> removeTodo(todo.id)}>
                <span class="icon">
                  <i class="fas fa-check"></i>
                </span>
              </button>
            </div>
          </li>
        {:else}
          <li class="Listo" transition:slide="{{delay: 600, duration: 300, easing: elasticInOut}}">You're Done!</li>
        {/each}
      </ul>
      </div>
    </div>
  </div>

  <div class="Contenedor">
  	<h4 class="Copy">©2020 - Asis Butros</h4>
  </div>
</main>