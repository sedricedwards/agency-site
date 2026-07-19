<script lang="ts">
	import { onMount } from 'svelte';

	const termLines = [
		{ t: '00:00.0', cls: 'cmd', text: '$ claude "port our electron app to tauri + sveltekit"' },
		{ t: '00:03.8', cls: 'info', text: '● scanning repository — 412 files mapped' },
		{ t: '00:11.2', cls: 'info', text: '● architecture plan approved · 37 components → svelte 5' },
		{ t: '00:26.5', cls: 'info', text: '● migrating runtime · wiring native apis' },
		{ t: '00:41.9', cls: 'ok', text: '✓ build passing · bundle 184 MB → 9.6 MB' },
		{ t: '00:52.3', cls: 'ok', text: '✓ deployed to production' },
		{ t: '——', cls: 'note', text: 'shipped in weeks — traditional estimate: two quarters' }
	];

	let shown = $state(0);
	let mounted = $state(false);

	onMount(() => {
		mounted = true;
		document.documentElement.classList.add('js');
		const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
		if (reduced) {
			shown = termLines.length;
		} else {
			let i = 0;
			const tick = () => {
				shown = ++i;
				if (i < termLines.length) setTimeout(tick, i === 1 ? 900 : 650);
			};
			setTimeout(tick, 600);
		}

		const io = new IntersectionObserver(
			(entries) => {
				for (const e of entries) {
					if (e.isIntersecting) {
						e.target.classList.add('in');
						io.unobserve(e.target);
					}
				}
			},
			{ threshold: 0.15 }
		);
		document.querySelectorAll('[data-reveal]').forEach((el) => io.observe(el));
		return () => io.disconnect();
	});

	let name = $state('');
	let email = $state('');
	let brief = $state('');

	function submit(e: SubmitEvent) {
		e.preventDefault();
		const subject = encodeURIComponent(`Velocity Session — ${name}`);
		const body = encodeURIComponent(`Name: ${name}\nEmail: ${email}\n\nProject brief:\n${brief}`);
		window.location.href = `mailto:sedric.edwards@gmail.com?subject=${subject}&body=${body}`;
	}

	const services = [
		{
			num: 'SVC-01',
			title: 'AI-Accelerated Web Apps',
			body: 'Custom application development using SvelteKit, TypeScript, and Tailwind CSS for clean, lightning-fast user experiences.'
		},
		{
			num: 'SVC-02',
			title: 'Architectural Migrations',
			body: 'Moving legacy desktop or web architectures to ultra-efficient, modern runtimes — like porting Electron apps to lightweight Tauri environments.'
		},
		{
			num: 'SVC-03',
			title: 'Product-to-Code Leadership',
			body: "Technical project management that eliminates communication friction. We don't just write code; we manage the roadmap."
		}
	];

	const stack = [
		{ label: 'Languages & Frameworks', items: ['SvelteKit', 'TypeScript', 'Node.js', 'Tailwind CSS'] },
		{ label: 'Desktop & Runtimes', items: ['Tauri', 'Electron'] },
		{ label: 'Acceleration Tools', items: ['Claude Code', 'Antigravity', 'Advanced AI Agent Workflows'] }
	];
</script>

<svelte:head>
	<title>High-Velocity Web Development — Sedric Edwards</title>
	<meta
		name="description"
		content="Senior-level software project management combined with AI-accelerated development to build, launch, and migrate web applications at a fraction of traditional timelines."
	/>
</svelte:head>

<!-- ─── Nav ─── -->
<header class="fixed inset-x-0 top-0 z-50 border-b border-line/70 bg-ink/80 backdrop-blur-md">
	<nav class="mx-auto flex h-16 max-w-6xl items-center justify-between px-5 sm:px-8">
		<a href="#top" class="font-mono text-[13px] font-medium tracking-widest text-fg">
			SEDRIC<span class="text-amber">·</span>EDWARDS
			<span class="ml-2 hidden text-dim sm:inline">/ HIGH-VELOCITY STUDIO</span>
		</a>
		<div class="flex items-center gap-6">
			<a href="#stack" class="hidden font-mono text-[12px] tracking-wider text-mute transition-colors hover:text-fg sm:inline">STACK</a>
			<a href="#services" class="hidden font-mono text-[12px] tracking-wider text-mute transition-colors hover:text-fg sm:inline">SERVICES</a>
			<a
				href="#contact"
				class="border border-amber/60 px-4 py-2 font-mono text-[12px] font-medium tracking-wider text-amber transition-colors hover:bg-amber hover:text-ink"
			>
				BOOK A SESSION
			</a>
		</div>
	</nav>
</header>

<main id="top" class="overflow-x-clip">
	<!-- ─── Hero ─── -->
	<section class="relative mx-auto grid max-w-6xl gap-14 px-5 pt-36 pb-24 sm:px-8 lg:grid-cols-[minmax(0,1.1fr)_minmax(0,0.9fr)] lg:items-center lg:gap-10 lg:pt-44 lg:pb-32">
		<div class="hero-grid" aria-hidden="true"></div>
		<div>
			<p class="eyebrow">T+00:00 · BRIEF RECEIVED</p>
			<h1 class="display mt-5 text-[clamp(2.3rem,5vw,3.9rem)] leading-[1.05] font-bold tracking-tight text-balance">
				<span class="whitespace-nowrap">High-Velocity</span> Web Development for
				<span class="whitespace-nowrap">Forward-Thinking</span> Teams.
			</h1>
			<p class="mt-6 max-w-xl text-[17px] leading-relaxed text-mute">
				We combine senior-level software project management with modern AI-accelerated development (Claude Code &amp;
				Google Antigravity) to build, launch, and migrate web applications at a fraction of traditional timelines.
			</p>
			<div class="mt-9 flex flex-wrap gap-4">
				<a href="#contact" class="btn-primary">Book a Velocity Session</a>
				<a href="#stack" class="btn-ghost">See Our Stack</a>
			</div>
		</div>

		<!-- signature: agent console -->
		<div class="term" aria-label="Simulated AI-agent build session">
			<div class="flex items-center justify-between border-b border-line px-4 py-2.5">
				<span class="font-mono text-[11px] tracking-wider text-dim">agent — migration.log</span>
				<span class="flex gap-1.5">
					<i class="h-2.5 w-2.5 rounded-full bg-line"></i>
					<i class="h-2.5 w-2.5 rounded-full bg-line"></i>
					<i class="h-2.5 w-2.5 rounded-full bg-amber/70"></i>
				</span>
			</div>
			<div class="min-h-[248px] p-4 font-mono text-[12.5px] leading-[1.9] sm:text-[13px]">
				{#each termLines.slice(0, shown) as line (line.t)}
					<p class="term-line {line.cls}">
						<span class="mr-3 text-dim select-none">{line.t}</span>{line.text}
					</p>
				{/each}
				{#if mounted && shown < termLines.length}
					<span class="cursor" aria-hidden="true"></span>
				{/if}
			</div>
		</div>
	</section>

	<!-- ─── Problem / Solution ─── -->
	<section class="border-t border-line">
		<div class="mx-auto max-w-6xl px-5 py-24 sm:px-8" data-reveal>
			<p class="eyebrow">T+00:12 · DIAGNOSIS</p>
			<div class="mt-10 grid gap-12 lg:grid-cols-2 lg:gap-16">
				<div class="border-l-2 border-line pl-6">
					<h2 class="display text-xl font-semibold tracking-tight text-dim">The Reality</h2>
					<p class="mt-4 text-[16px] leading-relaxed text-mute">
						Traditional software development takes too long, gets mired in endless scope creep, and breaks
						communication lines between product management and engineering.
					</p>
				</div>
				<div class="border-l-2 border-amber pl-6">
					<h2 class="display text-xl font-semibold tracking-tight">Our Approach</h2>
					<p class="mt-4 text-[16px] leading-relaxed text-mute">
						We bridge the gap. By leveraging advanced agentic workflows and developer tools, we collapse the timeline
						between architectural design and deployment—without sacrificing code quality or stability.
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- ─── Services ─── -->
	<section id="services" class="border-t border-line bg-panel/40">
		<div class="mx-auto max-w-6xl px-5 py-24 sm:px-8" data-reveal>
			<p class="eyebrow">T+01:30 · EXECUTION</p>
			<h2 class="display mt-5 text-3xl font-bold tracking-tight sm:text-4xl">Core Services</h2>
			<div class="mt-12 grid gap-px overflow-hidden border border-line bg-line lg:grid-cols-3">
				{#each services as s (s.num)}
					<article class="group bg-panel p-8 transition-colors duration-300 hover:bg-panel-2">
						<p class="font-mono text-[11px] tracking-widest text-dim transition-colors group-hover:text-amber">{s.num}</p>
						<h3 class="display mt-5 text-[19px] font-semibold tracking-tight">{s.title}</h3>
						<p class="mt-4 text-[15px] leading-relaxed text-mute">{s.body}</p>
					</article>
				{/each}
			</div>
		</div>
	</section>

	<!-- ─── Stack ─── -->
	<section id="stack" class="border-t border-line">
		<div class="mx-auto max-w-6xl px-5 py-24 sm:px-8" data-reveal>
			<p class="eyebrow">T+03:00 · TOOLING</p>
			<h2 class="display mt-5 text-3xl font-bold tracking-tight sm:text-4xl">The Stack &amp; Workflow</h2>
			<dl class="mt-12 divide-y divide-line border-y border-line">
				{#each stack as row (row.label)}
					<div class="grid gap-3 py-6 sm:grid-cols-[240px_1fr] sm:gap-8">
						<dt class="font-mono text-[12px] tracking-wider text-dim uppercase">{row.label}</dt>
						<dd class="flex flex-wrap gap-2.5">
							{#each row.items as item (item)}
								<span class="border border-line px-3 py-1.5 font-mono text-[12.5px] text-fg/90 transition-colors hover:border-amber/60 hover:text-amber">{item}</span>
							{/each}
						</dd>
					</div>
				{/each}
			</dl>
		</div>
	</section>

	<!-- ─── Contact ─── -->
	<section id="contact" class="border-t border-line bg-panel/40">
		<div class="mx-auto grid max-w-6xl gap-14 px-5 py-24 sm:px-8 lg:grid-cols-2 lg:gap-20" data-reveal>
			<div>
				<p class="eyebrow">T+04:45 · SHIP</p>
				<h2 class="display mt-5 text-3xl font-bold tracking-tight text-balance sm:text-4xl">
					Ready to build at the speed of thought?
				</h2>
				<p class="mt-5 max-w-md text-[16px] leading-relaxed text-mute">
					Let's map out your project requirements and show you what a velocity-driven workflow looks like.
				</p>
			</div>
			<form onsubmit={submit} class="grid gap-5">
				<label class="grid gap-2">
					<span class="font-mono text-[11px] tracking-widest text-dim uppercase">Name</span>
					<input required bind:value={name} type="text" autocomplete="name" class="field" />
				</label>
				<label class="grid gap-2">
					<span class="font-mono text-[11px] tracking-widest text-dim uppercase">Email</span>
					<input required bind:value={email} type="email" autocomplete="email" class="field" />
				</label>
				<label class="grid gap-2">
					<span class="font-mono text-[11px] tracking-widest text-dim uppercase">Project Brief</span>
					<textarea required bind:value={brief} rows="4" class="field resize-y"></textarea>
				</label>
				<button type="submit" class="btn-primary mt-1 justify-self-start">Book a Velocity Session</button>
			</form>
		</div>
	</section>

	<footer class="border-t border-line">
		<div class="mx-auto flex max-w-6xl flex-col items-start justify-between gap-3 px-5 py-8 font-mono text-[12px] text-dim sm:flex-row sm:items-center sm:px-8">
			<p>Copyright © 2026. Designed by Sedric Edwards.</p>
			<p>SEDRIC<span class="text-amber">·</span>EDWARDS / HIGH-VELOCITY STUDIO</p>
		</div>
	</footer>
</main>

<style>
	.eyebrow {
		font-family: var(--font-mono);
		font-size: 11.5px;
		letter-spacing: 0.18em;
		color: var(--color-amber);
	}

	.display {
		font-family: var(--font-display);
		font-variation-settings: 'wdth' 112;
	}

	.btn-primary,
	.btn-ghost {
		display: inline-flex;
		align-items: center;
		padding: 0.85rem 1.6rem;
		font-family: var(--font-mono);
		font-size: 13px;
		font-weight: 500;
		letter-spacing: 0.06em;
		transition:
			background-color 0.2s,
			color 0.2s,
			border-color 0.2s;
	}
	.btn-primary {
		background: var(--color-amber);
		color: var(--color-ink);
		border: 1px solid var(--color-amber);
	}
	.btn-primary:hover {
		background: transparent;
		color: var(--color-amber);
	}
	.btn-ghost {
		border: 1px solid var(--color-line);
		color: var(--color-fg);
	}
	.btn-ghost:hover {
		border-color: var(--color-amber);
		color: var(--color-amber);
	}

	.field {
		background: var(--color-ink);
		border: 1px solid var(--color-line);
		color: var(--color-fg);
		padding: 0.75rem 0.9rem;
		font-size: 15px;
		transition: border-color 0.2s;
	}
	.field:focus {
		outline: none;
		border-color: var(--color-amber);
	}

	.term {
		border: 1px solid var(--color-line);
		background: var(--color-panel);
		box-shadow: 0 0 80px rgb(255 180 84 / 0.05);
	}
	.term-line {
		animation: rise 0.35s ease both;
	}
	.term-line.cmd {
		color: var(--color-fg);
	}
	.term-line.info {
		color: var(--color-mute);
	}
	.term-line.ok {
		color: var(--color-ok);
	}
	.term-line.note {
		color: var(--color-amber);
		margin-top: 0.5rem;
	}
	.cursor {
		display: inline-block;
		width: 8px;
		height: 15px;
		background: var(--color-amber);
		animation: blink 1s steps(1) infinite;
		vertical-align: text-bottom;
	}

	.hero-grid {
		position: absolute;
		inset: 0;
		pointer-events: none;
		background-image:
			linear-gradient(rgb(27 36 50 / 0.35) 1px, transparent 1px),
			linear-gradient(90deg, rgb(27 36 50 / 0.35) 1px, transparent 1px);
		background-size: 56px 56px;
		mask-image: radial-gradient(ellipse 90% 70% at 50% 0%, black 30%, transparent 75%);
	}

	/* reveal only when JS is confirmed present, so content is never lost without it */
	:global(html.js [data-reveal]) {
		opacity: 0;
		transform: translateY(18px);
		transition:
			opacity 0.7s ease,
			transform 0.7s ease;
	}
	:global(html.js [data-reveal].in) {
		opacity: 1;
		transform: none;
	}
	@media (prefers-reduced-motion: reduce) {
		:global(html.js [data-reveal]) {
			opacity: 1;
			transform: none;
		}
	}

	@keyframes rise {
		from {
			opacity: 0;
			transform: translateY(6px);
		}
		to {
			opacity: 1;
			transform: none;
		}
	}
	@keyframes blink {
		50% {
			opacity: 0;
		}
	}
</style>
