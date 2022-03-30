<template>
	<div id="app">
		<div id="nav">
			<div id="popup">
				<div id="main-body">
					<div>Hello.
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
export default {
}
</script>
<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}

#nav {
	padding: 30px;
}

#nav a {
	font-weight: bold;
	padding: 5px;
	text-decoration: none;
	color: #2c3e50;
}

#nav a.router-link-exact-active {
	color: #42b983;
}

#nav > button {
	padding: 0.6rem 1rem;
	cursor: pointer;
	background: #fff;
	border: 1px solid #ccc;
	border-radius: 50px;
	width: 5rem;
	outline: none;
	transition: 0.3s;
	margin: 0 auto;
	font-size: 14px;
	font-weight: bold;
}

#nav > button:hover {
	background-color: #42b983;
	color: white;
}
</style>
