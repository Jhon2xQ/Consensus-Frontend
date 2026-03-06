<script lang="ts">
	import { authClient } from "$lib/auth-client";
	import { goto } from "$app/navigation";

	const session = authClient.useSession();

	let email = $state("");
	let password = $state("");
	let error = $state("");
	let loading = $state(false);

	async function handleSignIn() {
		loading = true;
		error = "";
		const { data, error: err } = await authClient.signIn.email({
			email,
			password
		}, {
			onSuccess: () => {
				goto("/");
			}
		});
		loading = false;
		if (err) {
			error = err.message ?? "Error al iniciar sesión";
		}
	}
</script>

<svelte:head>
	<title>Iniciar sesión - Consensus</title>
</svelte:head>

<div class="min-h-screen flex items-center justify-center bg-gray-50 px-4">
	<div class="max-w-md w-full space-y-8">
		<div class="text-center">
			<h2 class="text-3xl font-bold text-gray-900">Iniciar sesión</h2>
			<p class="mt-2 text-sm text-gray-600">
				O <a href="/signup" class="font-medium text-indigo-600 hover:text-indigo-500">crea una cuenta</a>
			</p>
		</div>

		<form class="mt-8 space-y-6" onsubmit={(e) => { e.preventDefault(); handleSignIn(); }}>
			<div class="space-y-4">
				<div>
					<label for="email" class="block text-sm font-medium text-gray-700">Email</label>
					<input
						id="email"
						type="email"
						bind:value={email}
						required
						class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
						placeholder="tu@email.com"
					/>
				</div>
				<div>
					<label for="password" class="block text-sm font-medium text-gray-700">Contraseña</label>
					<input
						id="password"
						type="password"
						bind:value={password}
						required
						class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
						placeholder="••••••••"
					/>
				</div>
			</div>

			{#if error}
				<div class="text-sm text-red-600 text-center">{error}</div>
			{/if}

			<button
				type="submit"
				disabled={loading}
				class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 disabled:opacity-50"
			>
				{loading ? "Iniciando..." : "Iniciar sesión"}
			</button>
		</form>
	</div>
</div>
