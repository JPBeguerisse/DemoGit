<!-- App.svelte -->
<script>
  import Router from 'svelte-spa-router';
  import Route from 'svelte-spa-router';

  import TaskList from './component/TaskList.svelte'
  import TaskDetail from './component/TaskDetail.svelte'
</script>

<!-- <Router>
  <Route path="/" component={TaskList} />
  <Route path="/task/:taskId" component={TaskDetail} />
</Router> -->


<Router routes={{
	'/': TaskList,
	'/list/:id': TaskDetail,
}} />


