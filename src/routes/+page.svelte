<script lang="ts">
  import { PUBLIC_API_URL } from "$env/static/public";
	import { authClient } from "$lib/auth-client";
	const session = authClient.useSession();

	let apiData = $state<{ success: boolean; message: string; data: unknown; timestamp: number } | null>(null);
	let apiLoading = $state(false);
	let apiError = $state("");

	async function fetchPrivateData() {
		apiLoading = true;
		apiError = "";
		try {
			const response = await fetch(`${PUBLIC_API_URL}/api/example/private`, {
				credentials: "include"
			});
			const data = await response.json();
			apiData = data;
		} catch (err) {
			apiError = "Error al conectar con el servidor";
			apiData = null;
		}
		apiLoading = false;
	}

	$effect(() => {
		if ($session.data) {
			fetchPrivateData();
		} else {
			apiData = null;
		}
	});

	async function handleSignOut() {
		await authClient.signOut();
	}
</script>

<svelte:head>
	<title>Consensus</title>
</svelte:head>

<div class="min-h-screen bg-gray-50">
	<header class="bg-white shadow">
		<div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8 flex justify-between items-center">
			<h1 class="text-3xl font-bold text-gray-900">Consensus</h1>
			{#if $session.data}
				<div class="flex items-center gap-4">
					<div class="text-right">
						<p class="text-sm font-medium text-gray-900">{$session.data.user.name ?? "Usuario"}</p>
						<p class="text-xs text-gray-500">{$session.data.user.email}</p>
					</div>
					<button
						onclick={handleSignOut}
						class="text-sm text-red-600 hover:text-red-700"
					>
						Cerrar sesión
					</button>
				</div>
			{:else}
				<div class="flex items-center gap-3">
					<a
						href="/login"
						class="text-sm text-gray-700 hover:text-gray-900"
					>
						Iniciar sesión
					</a>
					<a
						href="/signup"
						class="text-sm bg-indigo-600 text-white px-4 py-2 rounded-md hover:bg-indigo-700"
					>
						Registrarse
					</a>
				</div>
			{/if}
		</div>
	</header>

	<main class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
		{#if $session.data}
			<div class="px-4 py-6 sm:px-0 space-y-4">
				<div class="bg-white rounded-lg shadow px-5 py-6">
					<h2 class="text-xl font-semibold text-gray-900 mb-4">Bienvenido, {$session.data.user.name ?? "Usuario"}</h2>
					<p class="text-gray-600">Email: {$session.data.user.email}</p>
					<p class="text-gray-500 text-sm mt-2">Sesión activa</p>
				</div>

				<div class="bg-white rounded-lg shadow px-5 py-6">
					<h3 class="text-lg font-semibold text-gray-900 mb-4">Datos del Backend</h3>
					
					{#if apiLoading}
						<p class="text-gray-500">Cargando...</p>
					{:else if apiError}
						<p class="text-red-600">{apiError}</p>
					{:else if apiData}
						{#if apiData.success}
							<div class="p-3 bg-green-50 border border-green-200 rounded-md">
								<p class="text-green-800 font-medium">{apiData.message}</p>
								{#if apiData.data}
									<pre class="mt-2 text-sm text-green-700 whitespace-pre-wrap">{JSON.stringify(apiData.data, null, 2)}</pre>
								{/if}
							</div>
						{:else}
							<div class="p-3 bg-red-50 border border-red-200 rounded-md">
								<p class="text-red-800 font-medium">{apiData.message}</p>
							</div>
						{/if}
					{/if}
				</div>
			</div>
		{:else}
			<div class="px-4 py-6 sm:px-0 text-center">
				<p class="text-lg text-gray-600 mb-4">¿Ya tienes una cuenta?</p>
				<a
					href="/login"
					class="inline-block bg-indigo-600 text-white px-6 py-3 rounded-md hover:bg-indigo-700 mr-4"
				>
					Iniciar sesión
				</a>
				<a
					href="/signup"
					class="inline-block bg-white text-indigo-600 border border-indigo-600 px-6 py-3 rounded-md hover:bg-indigo-50"
				>
					Registrarse
				</a>
			</div>
		{/if}
	</main>
</div>
