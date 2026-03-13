<script lang="ts">
	let { class: className = '' } = $props<{ class?: string }>();
</script>

<footer class="bg-slate-950 border-t border-slate-800/50 pt-28 pb-12 relative overflow-hidden {className}">
	<div class="absolute bottom-0 left-0 right-0 h-96 bg-gradient-to-t from-emerald-950/10 to-transparent pointer-events-none"></div>
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 relative z-10">
		<div class="grid grid-cols-1 md:grid-cols-12 gap-16 mb-24">
			<div class="col-span-1 md:col-span-5">
				<div class="flex items-center gap-3 mb-8">
					<div class="relative flex h-11 w-11 items-center justify-center rounded-xl bg-gradient-to-br from-emerald-400 to-teal-600 shadow-lg shadow-emerald-500/20">
						<span class="material-symbols-outlined text-white text-[26px]">how_to_vote</span>
					</div>
					<span class="text-2xl font-bold tracking-tight text-white">Consensus</span>
				</div>
				<p class="text-slate-500 max-w-sm text-base leading-relaxed mb-10">
					Plataforma de investigación académica dedicada a la implementación de sistemas de votación privada mediante tecnología blockchain.
				</p>
				<div class="flex gap-4">
					<a class="flex h-11 w-11 items-center justify-center rounded-xl bg-slate-800/50 text-slate-400 hover:text-white hover:bg-slate-800 transition-all border border-slate-700/50" href="https://github.com" aria-label="GitHub">
						<svg class="h-5 w-5" fill="currentColor" viewBox="0 0 24 24">
							<path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
						</svg>
					</a>
					<a class="flex h-11 w-11 items-center justify-center rounded-xl bg-slate-800/50 text-slate-400 hover:text-white hover:bg-slate-800 transition-all border border-slate-700/50" href="mailto:contact@consensus.edu" aria-label="Email">
						<span class="material-symbols-outlined text-[22px]">mail</span>
					</a>
				</div>
			</div>
			
			<div class="col-span-1 md:col-span-2">
				<h4 class="text-white font-bold mb-8 text-xs uppercase tracking-[0.2em]">Navegación</h4>
				<ul class="space-y-4 text-sm">
					<li><a class="text-slate-500 hover:text-emerald-400 transition-colors flex items-center group gap-2" href="/procesos">Procesos</a></li>
					<li><a class="text-slate-500 hover:text-emerald-400 transition-colors flex items-center group gap-2" href="/sobre">Sobre nosotros</a></li>
					<li><a class="text-slate-500 hover:text-emerald-400 transition-colors flex items-center group gap-2" href="/metodologia">Metodología</a></li>
				</ul>
			</div>
			
			<div class="col-span-1 md:col-span-2">
				<h4 class="text-white font-bold mb-8 text-xs uppercase tracking-[0.2em]">Recursos</h4>
				<ul class="space-y-4 text-sm">
					<li><a class="text-slate-500 hover:text-emerald-400 transition-colors flex items-center group gap-2" href="/docs">Documentación</a></li>
					<li><a class="text-slate-500 hover:text-emerald-400 transition-colors flex items-center group gap-2" href="https://github.com" aria-label="Repositorio">Repositorio</a></li>
					<li><a class="text-slate-500 hover:text-emerald-400 transition-colors flex items-center group gap-2" href="/privacidad">Privacidad</a></li>
				</ul>
			</div>
			
			<div class="col-span-1 md:col-span-3">
				<div class="bg-slate-800/30 border border-slate-700/50 rounded-2xl p-6 backdrop-blur-sm">
					<div class="flex items-center gap-2 mb-4">
						<span class="h-2 w-2 rounded-full bg-emerald-500 animate-pulse"></span>
						<span class="text-[10px] font-bold text-emerald-500/80 uppercase tracking-widest">Estado del Sistema</span>
					</div>
					<p class="text-xs text-slate-500 leading-relaxed">
						Todos los nodos operativos. Protocolo Semaphore V2 activo en la red principal.
					</p>
				</div>
			</div>
		</div>
		
		<div class="flex flex-col md:flex-row items-center justify-between border-t border-slate-800/50 pt-10 gap-6">
			<p class="text-slate-600 text-xs font-medium tracking-tight">© 2024 Proyecto Consensus. Desarrollado para entornos académicos y profesionales.</p>
			<div class="flex items-center gap-6">
				<a class="text-xs text-slate-600 hover:text-white transition-colors" href="/terminos">Términos</a>
				<a class="text-xs text-slate-600 hover:text-white transition-colors" href="/cookies">Cookies</a>
			</div>
		</div>
	</div>
</footer>
