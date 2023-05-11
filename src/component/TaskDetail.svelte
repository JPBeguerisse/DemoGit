<script>
  import { onMount } from 'svelte';
  import { push } from 'svelte-spa-router';

  export let params;
  let lists = JSON.parse(localStorage.getItem('lists')) || [];

  let list;
  let newtaskTitle = '';

  
  //ajout de sous tache
  function addSubtask(event){
    event.preventDefault();

    //creation d'un sous tache
    const newTask = {
      id: Date.now(), // l'id de sous tache sera la dateheure lors du clique
      title: newtaskTitle.trim(), // le titre sera les données entrer dans le champs newTaskTitle
      completed: false
    };

    if(newtaskTitle.trim() === '') 
      return;

      if (!list.subtasks) {
        list.subtasks = []; // initialiser le tableau de sous-tâches qui sera stocker dans la list en question
      }
    
      if(newTask)
      {
         //console.log(newTask);
        //ajouter le sous tache dans un propriété subTask de list
        list.subtasks.push(newTask);
        //console.log(list);

        localStorage.setItem('lists', JSON.stringify(lists));
        newtaskTitle = '';
        //console.log(list.subtasks);
      }

   

  }


  onMount(() => {
    //recherche la list dans le localstorage via son id récuéperer en params 
    list = lists.find(l => l.id === Number(params.id));
    // console.log(params.id);
    // console.log(list.title);
    
  });
</script>


<form on:submit={addSubtask}>
  <input type="text" bind:value={newtaskTitle}>
  <button type="submit">Add subtask</button>
</form>


<!-- Afficher le titre de la liste -->
{#if list}
  <h1>{list.title}</h1>
  <ul>
    {#each list.subtasks as subtask}
      <li>{subtask.title}</li>
    {/each}
    </ul>
{/if}
