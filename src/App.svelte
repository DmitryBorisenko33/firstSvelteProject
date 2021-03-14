<script>
	import { Route, router, active } from "tinro";
	import { toast } from "@zerodevx/svelte-toast";
	let setMain = "Устройство";
	let setWifi = "WiFi";
	let setMqtt = "MQTT";
	let result = null;
	let inputValue;
	let st = "1";
	function submitHandler() {
		console.log("лог", inputValue);
	}

	async function doGetRequest() {
		if (st == "1") {
			st = "0";
		} else if (st == "0") {
			st = "1";
		}

		let res = await fetch("http://192.168.88.16/set?order=btn640_" + st, {
			mode: "no-cors",
			method: "GET",
		});

		if (res.ok) {
			let text = await response.text();
			alert("text " + text.slice(0, 80) + "...");
		} else {
			alert("status " + res.status);
		}
	}
</script>

<div class="hamburger-menu">
	<input id="menu__toggle" type="checkbox" />
	<label class="menu__btn" for="menu__toggle">
		<span />
	</label>
	<ul class="menu__box">
		<li><a class="menu__item" href="/">{setMain}</a></li>
		<li><a class="menu__item" href="/wifi">{setWifi}</a></li>
		<li><a class="menu__item" href="/mqtt">{setMqtt}</a></li>
	</ul>

	<ul class="menu__main">
		<Route path="/">
			<div class="head">
				<h2>{setMain}</h2>
				<button type="button" on:click={doGetRequest}
					>Get request</button
				>
				<button
					type="button"
					on:click={() => toast.push("Hello world!")}
					>EMIT TOAST</button
				>
				<p>Result:</p>
				<pre>
				{result}
				</pre>
			</div>
		</Route>

		<Route path="/wifi">
			<div class="head">
				<h2>{setWifi}</h2>
			</div>

			<div class="content">
				<div class="box">
					<slot>
						<form>
							<div class="row">
								<div class="left-column">
									<label for="fname">Название сети:</label>
								</div>
								<div class="right-column">
									<input
										type="text"
										id="fname"
										name="fname"
									/>
								</div>
							</div>

							<div class="row">
								<div class="left-column">
									<label for="lname">Пароль:</label>
								</div>
								<div class="right-column">
									<input
										type="password"
										id="lname"
										name="lname"
									/>
								</div>
							</div>

							<div class="row">
								<div class="center-column">
									<button
										type="button"
										on:click={submitHandler}
										>Сохранить
									</button>
								</div>
							</div>
						</form>
					</slot>
				</div>
			</div>
		</Route>

		<Route path="/mqtt">
			<div class="head">
				<h2>{setMqtt}</h2>
			</div>
		</Route>
	</ul>
</div>

<style>
	#menu__toggle {
		opacity: 0;
	}

	#menu__toggle:checked ~ .menu__btn > span {
		transform: rotate(45deg);
	}
	#menu__toggle:checked ~ .menu__btn > span::before {
		top: 0;
		transform: rotate(0);
	}
	#menu__toggle:checked ~ .menu__btn > span::after {
		top: 0;
		transform: rotate(90deg);
	}
	#menu__toggle:checked ~ .menu__box {
		visibility: visible;
		left: 0;
	}
	#menu__toggle:checked ~ .menu__main {
		margin-left: 150px;
	}

	.menu__btn {
		display: flex;
		align-items: center;
		position: fixed;
		top: 20px;
		left: 20px;
		width: 26px;
		height: 26px;
		cursor: pointer;
		z-index: 1;
	}

	.menu__btn > span,
	.menu__btn > span::before,
	.menu__btn > span::after {
		display: block;
		position: absolute;
		width: 100%;
		height: 2px;
		background-color: #616161;
		transition-duration: 0.25s;
	}
	.menu__btn > span::before {
		content: "";
		top: -8px;
	}
	.menu__btn > span::after {
		content: "";
		top: 8px;
	}

	.menu__box {
		display: block;
		position: fixed;
		visibility: hidden;
		top: 0;
		left: -100%;
		width: 150px; /* размер выхода бокового меню */
		height: 100%;
		margin: 0;
		padding: 80px 0;
		list-style: none;
		background-color: #eceff1;
		box-shadow: 1px 0px 6px rgba(0, 0, 0, 0.2);
		transition-duration: 0.25s;
	}

	.menu__item {
		display: block;
		padding: 12px 24px;
		color: #333;
		font-family: "Roboto", sans-serif;
		font-size: 15px; /* размер шрифта бокового меню */
		font-weight: 600;
		text-decoration: none;
		transition-duration: 0.25s;
	}
	.menu__item:hover {
		background-color: #cfd8dc;
	}

	.head {
		text-align: center;
		color: #000000;
		display: block;
	}

	.content {
		color: #000000;
		display: block;
	}

	.box {
		margin: 10px auto 10px;
		width: 50%;
		height: 100%;
		border: 1px solid #aaa;
		border-radius: 2px;
		box-shadow: 10px 10px 20px rgba(0, 0, 0, 0.1);
		padding: 1em;
	}

	.row {
		margin-top: 2%;
		margin-bottom: 2%;
		margin-right: 5%;
		margin-left: 5%;
	}

	.left-column {
		display: inline-block;
		width: 50%;
	}

	.right-column {
		display: inline-block;
	}

	.center-column {
		display: block;
		text-align: center;
	}

	input {
		min-width: 100px;
		max-width: 600px;
	}

	label {
		display: flex;
	}
</style>
