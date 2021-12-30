<script>
	export let showForm;
</script>

<!-- HTML -->
<nav class="nav">
	<div class="nav-center">
		<h1 class="nav-title">Budget calculator</h1>
		<button class="nav-btn" type="submit" on:click={showForm}>
			<i class="far fa-plus-square"/>
			Add item
		</button>
	</div>
</nav>