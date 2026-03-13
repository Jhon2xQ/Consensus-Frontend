<script lang="ts">
	let { class: className = '' } = $props<{ class?: string }>();
</script>

<nav class="fixed top-0 left-0 right-0 z-50 w-full glass-nav {className}">
	<div class="absolute inset-0 bg-gradient-to-b from-slate-950/80 to-slate-950/40 backdrop-blur-xl"></div>
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 relative z-10">
		<div class="flex h-16 items-center justify-between">
			<a href="/" class="flex items-center gap-3 group cursor-pointer">
				<div class="relative flex h-10 w-10 items-center justify-center rounded-xl bg-gradient-to-br from-emerald-400 via-teal-500 to-cyan-600 shadow-lg shadow-emerald-500/20 group-hover:scale-105 transition-all duration-300">
					<span class="material-symbols-outlined text-white text-[24px] font-bold">how_to_vote</span>
				</div>
				<span class="text-xl font-bold tracking-tight text-white">Consensus</span>
			</a>
			
			<div class="hidden md:flex items-center gap-8">
				<a class="nav-link text-sm font-medium text-slate-300 hover:text-white transition-colors" href="/">Inicio</a>
				<a class="nav-link text-sm font-medium text-slate-300 hover:text-white transition-colors" href="/procesos">Procesos</a>
				<a class="nav-link text-sm font-medium text-slate-300 hover:text-white transition-colors" href="/sobre">Sobre el Proyecto</a>
				<a class="nav-link text-sm font-medium text-slate-300 hover:text-white transition-colors" href="/docs">Documentación</a>
			</div>
			
			<div class="flex items-center gap-3">
				<button class="relative group h-10 flex items-center justify-center rounded-xl bg-gradient-to-r from-emerald-500 to-teal-600 px-6 text-sm font-bold text-white shadow-lg shadow-emerald-500/30 hover:shadow-emerald-500/50 transition-all hover:-translate-y-0.5 active:translate-y-0">
					Iniciar sesión
				</button>
			</div>
		</div>
	</div>
</nav>

<style>
	.glass-nav {
		border-bottom: 1px solid rgba(16, 185, 129, 0.1);
	}
	
	.nav-link {
		position: relative;
	}
	.nav-link::after {
		content: '';
		position: absolute;
		bottom: -4px;
		left: 50%;
		width: 0;
		height: 2px;
		background: linear-gradient(to right, #10b981, #14b8a6);
		transition: all 0.3s ease;
		transform: translateX(-50%);
		box-shadow: 0 0 8px rgba(16, 185, 129, 0.4);
	}
	.nav-link:hover::after {
		width: 100%;
	}
</style>
