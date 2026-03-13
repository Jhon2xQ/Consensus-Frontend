<script lang="ts">
	import Header from '$lib/components/custom/Header.svelte';
	import Footer from '$lib/components/custom/Footer.svelte';
</script>

<svelte:head>
	<title>Consensus - Plataforma de Votación Privada y Segura</title>
	<meta name="description" content="Plataforma de votación académica basada en protocolos de Zero-Knowledge. Garantizamos elecciones seguras, anónimas y verificables." />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="" />
	<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
	<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet" />
</svelte:head>

<Header />

<!-- Main Content -->
<main class="relative flex min-h-screen flex-col pt-16 bg-slate-950">
	<!-- Animated Background -->
	<div class="fixed inset-0 overflow-hidden pointer-events-none">
		<!-- Grid Pattern -->
		<div class="absolute inset-0 bg-[linear-gradient(to_right,#0f172a_1px,transparent_1px),linear-gradient(to_bottom,#0f172a_1px,transparent_1px)] bg-[size:4rem_4rem] [mask-image:radial-gradient(ellipse_80%_50%_at_50%_0%,#000_70%,transparent_110%)]"></div>
		
		<!-- Gradient Orbs -->
		<div class="absolute top-0 -left-4 w-96 h-96 bg-emerald-500 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-blob"></div>
		<div class="absolute top-0 -right-4 w-96 h-96 bg-teal-500 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-blob animation-delay-2000"></div>
		<div class="absolute -bottom-8 left-20 w-96 h-96 bg-cyan-500 rounded-full mix-blend-multiply filter blur-3xl opacity-20 animate-blob animation-delay-4000"></div>
		
		<!-- Rays -->
		<div class="absolute top-0 left-1/2 -translate-x-1/2 w-full h-[600px]">
			<div class="absolute inset-0 bg-gradient-to-b from-emerald-500/10 via-transparent to-transparent [mask-image:radial-gradient(ellipse_at_center,black_10%,transparent_70%)]"></div>
		</div>
	</div>
	
	<!-- Hero Section -->
	<section class="relative z-10 px-4 pt-20 pb-20 sm:px-6 lg:px-8 lg:pt-32">
		<div class="mx-auto max-w-7xl text-center">
			<!-- Active Process Badge -->
			<div class="mb-12 flex justify-center">
				<div class="active-process-pill flex items-center gap-4 p-1.5 pr-3 rounded-full max-w-xl group cursor-pointer backdrop-blur-md border border-emerald-500/20 bg-emerald-500/5 hover:bg-emerald-500/10 transition-all">
					<div class="bg-emerald-500/20 text-emerald-400 px-3 py-1.5 rounded-full flex items-center gap-2">
						<span class="relative flex h-2 w-2">
							<span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
							<span class="relative inline-flex rounded-full h-2 w-2 bg-emerald-400"></span>
						</span>
						<span class="text-[10px] font-bold uppercase tracking-wider">Activo</span>
					</div>
					<span class="text-sm font-semibold text-slate-200 truncate">Elecciones Consejo Universitario 2024</span>
					<div class="h-4 w-px bg-slate-700 mx-1"></div>
					<span class="text-xs font-bold text-emerald-400 flex items-center gap-1 uppercase tracking-tight group-hover:gap-2 transition-all">
						Participar
						<span class="material-symbols-outlined text-[16px]">arrow_forward</span>
					</span>
				</div>
			</div>
			
			<h1 class="hero-title mx-auto text-5xl font-bold text-white sm:text-7xl lg:text-8xl mb-8 leading-[1.1]">
				Democracia Digital con <br/>
				<span class="text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 via-teal-400 to-cyan-400 animate-gradient">Privacidad Absoluta</span>
			</h1>
			
			<p class="mx-auto max-w-3xl text-lg sm:text-xl text-slate-400 mb-16 leading-relaxed font-medium">
				Plataforma de votación académica basada en protocolos de <span class="text-emerald-400 font-semibold">Zero-Knowledge</span>. 
				Garantizamos elecciones seguras, anónimas y verificables.
			</p>
			
			<!-- Diagram -->
			<div class="relative mx-auto max-w-4xl rounded-3xl border border-slate-800/50 bg-slate-900/30 p-3 backdrop-blur-md shadow-2xl mb-24">
				<div class="relative rounded-2xl border border-slate-700/50 bg-slate-950/80 overflow-hidden">
					<div class="absolute inset-0 bg-gradient-to-b from-emerald-500/5 to-transparent"></div>
					<div class="relative p-12">
						<svg class="w-full h-auto max-w-[720px] mx-auto opacity-90" viewBox="0 0 800 240" xmlns="http://www.w3.org/2000/svg">
							<defs>
								<filter id="glow-svg" x="-25%" y="-25%" width="150%" height="150%">
									<feGaussianBlur stdDeviation="4" result="blur"/>
									<feComposite in="SourceGraphic" in2="blur" operator="over"/>
								</filter>
							</defs>
							
							<path d="M180 120 L320 120" stroke="#10b981" stroke-width="2" stroke-dasharray="10 5" opacity="0.3"/>
							<path d="M480 120 L620 120" stroke="#10b981" stroke-width="2" stroke-dasharray="10 5" opacity="0.3"/>
							
							<g transform="translate(100, 120)">
								<circle r="50" fill="#0f172a" stroke="rgba(16, 185, 129, 0.5)" stroke-width="2" filter="url(#glow-svg)"/>
								<text class="material-symbols-outlined" text-anchor="middle" y="12" font-size="32" fill="#10b981">fingerprint</text>
								<text text-anchor="middle" y="75" font-size="11" font-weight="bold" fill="#64748b">IDENTIDAD PRIVADA</text>
							</g>
							
							<g transform="translate(400, 120)">
								<rect x="-75" y="-55" width="150" height="110" rx="26" fill="#0f172a" stroke="#10b981" stroke-width="2.5" filter="url(#glow-svg)"/>
								<text class="material-symbols-outlined" text-anchor="middle" y="14" font-size="40" fill="#fff">security</text>
								<text text-anchor="middle" y="80" font-size="13" font-weight="black" fill="#fff">SEMAPHORE ZK</text>
							</g>
							
							<g transform="translate(700, 120)">
								<circle r="50" fill="#0f172a" stroke="rgba(16, 185, 129, 0.5)" stroke-width="2" filter="url(#glow-svg)"/>
								<text class="material-symbols-outlined" text-anchor="middle" y="12" font-size="32" fill="#10b981">verified</text>
								<text text-anchor="middle" y="75" font-size="11" font-weight="bold" fill="#64748b">VERIFICACIÓN</text>
							</g>
						</svg>
					</div>
				</div>
			</div>
		</div>
	</section>
	
	<!-- About Section -->
	<section class="relative z-10 py-32 bg-slate-900/50 border-y border-slate-800/50 overflow-hidden">
		<div class="absolute top-0 right-0 w-1/2 h-full bg-emerald-500/5 blur-[120px] pointer-events-none"></div>
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<div class="grid grid-cols-1 lg:grid-cols-2 gap-20 items-center">
				<div class="relative z-10">
					<span class="inline-block px-3 py-1.5 rounded-full bg-emerald-500/10 text-emerald-400 text-[11px] font-bold tracking-[0.2em] uppercase mb-6 border border-emerald-500/20">Misión del Proyecto</span>
					<h2 class="text-4xl sm:text-5xl font-bold text-white mb-8 leading-tight">Sobre Consensus: Votación Descentralizada</h2>
					<p class="text-slate-400 text-lg leading-relaxed mb-10">
						Consensus nace para resolver la tensión entre transparencia y secreto en los procesos democráticos académicos. Utilizamos protocolos de última generación para que tu voto sea anónimo, pero tu participación sea auditable.
					</p>
					
					<div class="grid sm:grid-cols-2 gap-6">
						<div class="p-6 rounded-2xl bg-slate-800/30 border border-slate-700/50 hover:border-emerald-500/30 transition-all backdrop-blur-sm">
							<div class="h-10 w-10 rounded-xl bg-emerald-500/10 flex items-center justify-center mb-4 border border-emerald-500/20">
								<span class="material-symbols-outlined text-emerald-400 text-[20px]">shield</span>
							</div>
							<h4 class="text-white font-bold text-base mb-2">Criptografía Avanzada</h4>
							<p class="text-sm text-slate-500 leading-relaxed">Protocolo Semaphore sobre Ethereum para anonimato total.</p>
						</div>
						
						<div class="p-6 rounded-2xl bg-slate-800/30 border border-slate-700/50 hover:border-emerald-500/30 transition-all backdrop-blur-sm">
							<div class="h-10 w-10 rounded-xl bg-emerald-500/10 flex items-center justify-center mb-4 border border-emerald-500/20">
								<span class="material-symbols-outlined text-emerald-400 text-[20px]">history_edu</span>
							</div>
							<h4 class="text-white font-bold text-base mb-2">Integridad Auditada</h4>
							<p class="text-sm text-slate-500 leading-relaxed">Resultados verificables por cualquier usuario en tiempo real.</p>
						</div>
					</div>
				</div>
				
				<div class="grid grid-cols-1 sm:grid-cols-2 gap-6 relative">
					<div class="glass-card p-10 rounded-3xl flex flex-col items-center text-center border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm">
						<div class="relative mb-6">
							<div class="absolute inset-0 bg-emerald-500 blur-2xl opacity-20"></div>
							<span class="material-symbols-outlined text-emerald-400 text-[56px] relative">lock_person</span>
						</div>
						<h4 class="text-white text-lg font-bold mb-3">100% Privado</h4>
						<p class="text-sm text-slate-500 leading-relaxed">La identidad del votante y el sentido del voto están criptográficamente desvinculados.</p>
					</div>
					
					<div class="glass-card p-10 rounded-3xl flex flex-col items-center text-center sm:mt-12 border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm">
						<div class="relative mb-6">
							<div class="absolute inset-0 bg-emerald-500 blur-2xl opacity-20"></div>
							<span class="material-symbols-outlined text-emerald-400 text-[56px] relative">hub</span>
						</div>
						<h4 class="text-white text-lg font-bold mb-3">Sin Intermediarios</h4>
						<p class="text-sm text-slate-500 leading-relaxed">La red descentralizada elimina puntos únicos de falla o manipulación centralizada.</p>
					</div>
				</div>
			</div>
		</div>
	</section>
	
	<!-- Technology Section -->
	<section class="relative z-10 py-32 bg-slate-950">
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<div class="mb-20 text-center">
				<h2 class="text-4xl sm:text-5xl font-bold text-white mb-5">Fundamentos Tecnológicos</h2>
				<p class="text-slate-400 max-w-2xl mx-auto text-lg font-medium">Infraestructura matemática que redefine la confianza digital.</p>
			</div>
			
			<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
				<div class="glass-card group flex flex-col rounded-3xl p-10 border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm hover:border-emerald-500/30 transition-all">
					<div class="mb-8 inline-flex h-14 w-14 items-center justify-center rounded-xl bg-slate-700/30 text-emerald-400 group-hover:bg-emerald-500 group-hover:text-white transition-all duration-300 border border-slate-600/50">
						<span class="material-symbols-outlined text-[28px]">security_update_good</span>
					</div>
					<h3 class="text-xl font-bold text-white mb-4">ZK-SNARKs</h3>
					<p class="text-slate-400 leading-relaxed text-sm">
						Permite demostrar la elegibilidad de voto sin revelar datos de identidad, protegiendo al usuario mediante pruebas de conocimiento cero.
					</p>
				</div>
				
				<div class="glass-card group flex flex-col rounded-3xl p-10 border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm hover:border-emerald-500/30 transition-all">
					<div class="mb-8 inline-flex h-14 w-14 items-center justify-center rounded-xl bg-slate-700/30 text-emerald-400 group-hover:bg-emerald-500 group-hover:text-white transition-all duration-300 border border-slate-600/50">
						<span class="material-symbols-outlined text-[28px]">analytics</span>
					</div>
					<h3 class="text-xl font-bold text-white mb-4">Verificación Universal</h3>
					<p class="text-slate-400 leading-relaxed text-sm">
						Cualquier participante puede corroborar matemáticamente la validez del escrutinio final sin comprometer el secreto del sufragio.
					</p>
				</div>
				
				<div class="glass-card group flex flex-col rounded-3xl p-10 border border-slate-700/50 bg-slate-800/30 backdrop-blur-sm hover:border-emerald-500/30 transition-all">
					<div class="mb-8 inline-flex h-14 w-14 items-center justify-center rounded-xl bg-slate-700/30 text-emerald-400 group-hover:bg-emerald-500 group-hover:text-white transition-all duration-300 border border-slate-600/50">
						<span class="material-symbols-outlined text-[28px]">account_tree</span>
					</div>
					<h3 class="text-xl font-bold text-white mb-4">Secret Sharing</h3>
					<p class="text-slate-400 leading-relaxed text-sm">
						Distribución de fragmentos de llaves criptográficas para garantizar que ningún administrador pueda manipular el proceso de forma unilateral.
					</p>
				</div>
			</div>
		</div>
	</section>
	
	<!-- Partners Section -->
	<section class="relative z-10 py-32 bg-slate-900/50 border-t border-slate-800/50">
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<h2 class="text-center text-[10px] font-bold text-slate-500 uppercase tracking-[0.3em] mb-16">Colaboradores Institucionales</h2>
			
			<div class="flex flex-wrap justify-center items-center gap-16 md:gap-32 opacity-60 hover:opacity-100 transition-all duration-700">
				<div class="flex flex-col items-center gap-4 group">
					<div class="h-24 w-24 rounded-3xl bg-slate-800/50 border border-slate-700/50 flex items-center justify-center font-bold text-3xl text-white group-hover:border-emerald-500/40 group-hover:bg-slate-800 transition-all">U</div>
					<span class="text-[10px] font-bold text-slate-500 tracking-widest uppercase group-hover:text-emerald-400 transition-colors">UNSAAC</span>
				</div>
				
				<div class="flex flex-col items-center gap-4 group">
					<div class="h-24 w-24 rounded-3xl bg-slate-800/50 border border-slate-700/50 flex items-center justify-center font-bold text-3xl text-white group-hover:border-emerald-500/40 group-hover:bg-slate-800 transition-all">E</div>
					<span class="text-[10px] font-bold text-slate-500 tracking-widest uppercase group-hover:text-emerald-400 transition-colors">EPG</span>
				</div>
				
				<div class="flex flex-col items-center gap-4 group">
					<div class="h-24 w-24 rounded-3xl bg-slate-800/50 border border-slate-700/50 flex items-center justify-center font-bold text-3xl text-white group-hover:border-emerald-500/40 group-hover:bg-slate-800 transition-all">E</div>
					<span class="text-[10px] font-bold text-slate-500 tracking-widest uppercase group-hover:text-emerald-400 transition-colors">EPIIS</span>
				</div>
			</div>
		</div>
	</section>
	
<Footer />
</main>

<style>
	:global(body) {
		font-family: 'Space Grotesk', system-ui, -apple-system, sans-serif;
		background: #020617;
	}
	
	:global(::-webkit-scrollbar) {
		width: 10px;
	}
	:global(::-webkit-scrollbar-track) {
		background: #0f172a;
	}
	:global(::-webkit-scrollbar-thumb) {
		background: #1e293b;
		border-radius: 5px;
	}
	:global(::-webkit-scrollbar-thumb:hover) {
		background: #10b981;
	}
	
	.hero-title {
		letter-spacing: -0.02em;
	}
	
	@keyframes gradient {
		0%, 100% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
	}
	
	.animate-gradient {
		background-size: 200% 200%;
		animation: gradient 3s ease infinite;
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
	
	.animation-delay-4000 {
		animation-delay: 4s;
	}
</style>
