<script>
	import { Route, router, active } from "tinro";
</script>

<nav>
	<div class="sidenav">
		<button on:click={() => router.goto("/")}>Главные настройки</button>
		<button on:click={() => router.goto("/wifi")}>Настройки WiFi</button>
	</div>
</nav>

<div class="head">
	<Route path="/">
		<h1>Главные настройки</h1>
	</Route>

	<Route path="/wifi">
		<h1>Настройки wifi</h1>
	</Route>
</div>

<style>
	.sidenav {
		height: 100%; /* Full-height: remove this if you want "auto" height */
		width: 200px; /* Set the width of the sidebar */
		position: fixed; /* Fixed Sidebar (stay in place on scroll) */
		z-index: 1; /* Stay on top */
		top: 0; /* Stay at the top */
		left: 0;
		background-color: rgba(17, 17, 17, 0.658); /* Black */
		overflow-x: hidden; /* Disable horizontal scroll */
		padding-top: 20px;
	}

	/* The navigation menu links */
	.sidenav button {
		/*text-align: center;*/
		margin: 10px auto 10px;
		width: 180px;
		padding: 6px 8px 6px 16px;
		text-decoration: none;
		font-size: 15px;
		color: #000000;
		display: block;
	}

	.head h1 {
		text-align: center;
		color: #000000;
		display: block;
	}

	.head {
		margin-left: 200px; /* Same as the width of the sidebar */
		padding: 0px 10px;
	}
</style>
