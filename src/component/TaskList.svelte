<script>
import { onDestroy, onMount } from 'svelte';
import Router from 'svelte-spa-router';
import urlSlug from "url-slug" ;
import { push } from 'svelte-spa-router';



let lists = JSON.parse(localStorage.getItem('lists')) || [];
 
function addTask(event) {
    event.preventDefault();

    const input = event.target.querySelector('input');
    //const newTask = input.value;
    const newTask = { 
      id: lists.length + 1,
      title: input.value,
      done: false
    };

    if (newTask) {
      lists = [...lists, newTask];
      input.value = '';

    // Sauvegarde des tâches dans le localStorage
    localStorage.setItem('lists', JSON.stringify(lists));
    }
  }

  onMount(() => {
    const savedTasks = localStorage.getItem('lists');
    if (savedTasks) {
      lists = JSON.parse(savedTasks);
    }
  });


  function removeTask(index) {
  lists = lists.filter((_, i) => i !== index);
  localStorage.setItem('lists', JSON.stringify(lists));
  }

 

  const goToTaskDetail = (taskId) => {
    push(`/list/${taskId}`);
  };


</script>

<main>
    <h1>Ma liste de tâches</h1>
    <form on:submit={addTask}>
      <label>
        Nouvelle tâche :
        <input type="text" name="task" />
      </label>
      <button type="submit">Ajouter</button>
    </form>
    <ul>
      {#each lists as task, i}
      <li>
        {task.title}
        <button on:click={() => goToTaskDetail(task.id)}>Voir</button>
        <button on:click={() => removeTask(i)}>Supprimer</button>
      </li>
    {/each}
    </ul>
  </main>
  
  <style>
    ul {
      list-style: none;
      margin: 0;
      padding: 0;
    }
  </style>
  