<script lang="ts">
	import Header from '$lib/components/custom/Header.svelte';
	import Footer from '$lib/components/custom/Footer.svelte';
	
	interface Process {
		id: string;
		title: string;
		status: 'active' | 'finalized';
		startDate: string;
		endDate: string;
		category: string;
		votes?: number;
	}
	
	const activeProcesses: Process[] = [
		{
			id: '1',
			title: 'Elecciones Consejo Universitario 2024',
			status: 'active',
			startDate: '01 Oct, 2024',
			endDate: '15 Oct, 2024',
			category: 'UNSAAC'
		},
		{
			id: '2',
			title: 'Votación Presupuesto Participativo EPIIS',
			status: 'active',
			startDate: '28 Sep, 2024',
			endDate: '10 Oct, 2024',
			category: 'EPIIS'
		}
	];
	
	const finalizedProcesses: Process[] = [
		{
			id: '3',
			title: 'Elección Decano Facultad de Ciencias',
			status: 'finalized',
			startDate: '20 Sep, 2024',
			endDate: '20 Sep, 2024',
			category: 'UNSAAC',
			votes: 9395
		},
		{
			id: '4',
			title: 'Consulta Reglamento de Tesis v2.0',
			status: 'finalized',
			startDate: '08 Sep, 2024',
			endDate: '08 Sep, 2024',
			category: 'UNSAAC',
			votes: 8782
		},
		{
			id: '5',
			title: 'Elección de Representantes Docentes',
			status: 'finalized',
			startDate: '15 Ago, 2024',
			endDate: '15 Ago, 2024',
			category: 'UNSAAC',
			votes: 6421
		}
	];
</script>

<svelte:head>
	<title>Procesos - Consensus</title>
	<meta name="description" content="Catálogo público de procesos electorales. Participa de forma segura y transparente en las decisiones de nuestra comunidad académica." />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="" />
	<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
	<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet" />
</svelte:head>

<Header />

<main class="relative flex min-h-screen flex-col pt-16 bg-slate-950">
	<!-- Animated Background -->
	<div class="fixed inset-0 overflow-hidden pointer-events-none">
		<div class="absolute inset-0 bg-[linear-gradient(to_right,#0f172a_1px,transparent_1px),linear-gradient(to_bottom,#0f172a_1px,transparent_1px)] bg-[size:4rem_4rem] [mask-image:radial-gradient(ellipse_80%_50%_at_50%_0%,#000_70%,transparent_110%)]"></div>
		<div class="absolute top-0 -left-4 w-96 h-96 bg-emerald-500 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-blob"></div>
		<div class="absolute top-0 -right-4 w-96 h-96 bg-teal-500 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-blob animation-delay-2000"></div>
	</div>
	
	<!-- Hero Section -->
	<section class="relative z-10 px-4 pt-20 pb-16 sm:px-6 lg:px-8">
		<div class="mx-auto max-w-7xl">
			<div class="mb-6">
				<span class="inline-block px-3 py-1.5 rounded-full bg-emerald-500/10 text-emerald-400 text-[11px] font-bold tracking-[0.2em] uppercase border border-emerald-500/20">
					Catálogo Público
				</span>
			</div>
			<h1 class="text-5xl sm:text-6xl font-bold text-white mb-6 leading-tight">
				Lista de Procesos
			</h1>
			<p class="text-lg text-slate-400 max-w-3xl leading-relaxed">
				Mostrando los procesos más recientes. Participa de forma segura y transparente en las decisiones de nuestra comunidad académica.
			</p>
		</div>
	</section>
	
	<!-- Active Processes Section -->
	<section class="relative z-10 px-4 pb-12 sm:px-6 lg:px-8">
		<div class="mx-auto max-w-7xl">
			<div class="space-y-6">
				{#each activeProcesses as process (process.id)}
					<div class="group relative rounded-3xl border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm p-8 hover:border-emerald-500/30 transition-all">
						<div class="flex flex-col lg:flex-row lg:items-center lg:justify-between gap-6">
							<div class="flex-1">
								<div class="flex items-center gap-3 mb-4">
									<div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-emerald-500/20 border border-emerald-500/30">
										<span class="relative flex h-2 w-2">
											<span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
											<span class="relative inline-flex rounded-full h-2 w-2 bg-emerald-400"></span>
										</span>
										<span class="text-[10px] font-bold uppercase tracking-wider text-emerald-400">Activo</span>
									</div>
									<span class="text-xs font-bold text-slate-500 uppercase tracking-wider">{process.category}</span>
								</div>
								
								<h3 class="text-2xl font-bold text-white mb-3 group-hover:text-emerald-400 transition-colors">
									{process.title}
								</h3>
								
								<div class="flex flex-wrap items-center gap-4 text-sm text-slate-400">
									<div class="flex items-center gap-2">
										<span class="material-symbols-outlined text-[18px]">calendar_today</span>
										<span>Inicio: {process.startDate}</span>
									</div>
									<div class="flex items-center gap-2">
										<span class="material-symbols-outlined text-[18px]">event</span>
										<span>Cierre: {process.endDate}</span>
									</div>
								</div>
							</div>
							
							<div class="flex items-center">
								<button class="flex items-center gap-2 px-6 py-3 rounded-xl bg-gradient-to-r from-emerald-500 to-teal-600 text-white font-bold text-sm shadow-lg shadow-emerald-500/30 hover:shadow-emerald-500/50 transition-all hover:-translate-y-0.5">
									Participar ahora
									<span class="material-symbols-outlined text-[18px]">arrow_forward</span>
								</button>
							</div>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>
	
	<!-- Finalized Processes Section -->
	<section class="relative z-10 px-4 py-16 sm:px-6 lg:px-8">
		<div class="mx-auto max-w-7xl">
			<div class="mb-12">
				<h2 class="text-3xl font-bold text-white mb-3">Últimos 10 procesos mostrados</h2>
			</div>
			
			<div class="space-y-6">
				{#each finalizedProcesses as process (process.id)}
					<div class="group relative rounded-3xl border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm p-8 hover:border-slate-600/50 transition-all">
						<div class="flex flex-col lg:flex-row lg:items-center lg:justify-between gap-6">
							<div class="flex-1">
								<div class="flex items-center gap-3 mb-4">
									<div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-700/50 border border-slate-600/50">
										<span class="text-[10px] font-bold uppercase tracking-wider text-slate-400">Finalizado</span>
									</div>
									<span class="text-xs font-bold text-slate-500 uppercase tracking-wider">ID: #{process.id}</span>
									<span class="text-xs font-bold text-slate-500 uppercase tracking-wider">{process.category}</span>
								</div>
								
								<h3 class="text-2xl font-bold text-white mb-3">
									{process.title}
								</h3>
								
								<div class="flex items-center gap-2 text-sm text-slate-400">
									<span class="material-symbols-outlined text-[18px]">schedule</span>
									<span>Finaliza el {process.endDate}</span>
								</div>
							</div>
							
							<div class="flex items-center">
								<button class="flex items-center gap-2 px-6 py-3 rounded-xl border border-slate-600/50 bg-slate-700/30 text-slate-300 font-bold text-sm hover:bg-slate-700/50 hover:border-slate-500/50 transition-all">
									Ver resultados
									<span class="material-symbols-outlined text-[18px]">open_in_new</span>
								</button>
							</div>
						</div>
					</div>
				{/each}
			</div>
			
			<!-- Load More Button -->
			<div class="mt-12 flex justify-center">
				<button class="flex items-center gap-2 px-8 py-4 rounded-xl border border-slate-700/50 bg-slate-800/30 text-slate-300 font-bold text-sm hover:bg-slate-800/50 hover:border-emerald-500/30 hover:text-emerald-400 transition-all backdrop-blur-sm">
					Cargar procesos anteriores
					<span class="material-symbols-outlined text-[18px]">expand_more</span>
				</button>
			</div>
		</div>
	</section>
</main>

<Footer />

<style>
	:global(body) {
		font-family: 'Space Grotesk', system-ui, -apple-system, sans-serif;
		background: #020617;
	}
	
	@keyframes blob {
		0%, 100% {
			transform: translate(0, 0) scale(1);
		}
		33% {
			transform: translate(30px, -50px) scale(1.1);
		}
		66% {
			transform: translate(-20px, 20px) scale(0.9);
		}
	}
	
	.animate-blob {
		animation: blob 7s infinite;
	}
	
	.animation-delay-2000 {
		animation-delay: 2s;
	}
</style>
