<script>
	const eventos = [
		{ date: "2026-01-16", title: "Examen – Primera Opción", type: "examen" },
		{ date: "2026-02-02", title: "Examen – Segunda Opción", type: "examen" },
		{ date: "2026-02-12", title: "Examen – Tercera Opción", type: "examen" }
	];

	const anuncios = [
		{
			title: "Publicación de Resultados",
			date: "2025-12-15",
			important: true,
			content: "Los resultados serán publicados a horas 21:00 del día lunes 15 de diciembre de 2025 en la página de admisión."
		},
		{
			title: "Presentación de Reclamos",
			date: "2025-12-17",
			important: false,
			content: "Los reclamos se recibirán hasta horas 15:00 del día miércoles 17 de diciembre de 2025 en la Dirección Académica."
		}
	];

	function formatDate(date) {
		return new Date(date).toLocaleDateString("es-BO", {
			day: "numeric",
			month: "long",
			year: "numeric"
		});
	}
</script>

<section class="page">
	<!-- NAVEGACIÓN LATERAL -->
	<nav class="side-nav">
		<a href="#calendario">📅 Calendario</a>
		<a href="#destacados">🔥 Últimos anuncios</a>
		<a href="#todos">📢 Todos los anuncios</a>
	</nav>

	<!-- CONTENIDO -->
	<div class="content">

		<!-- CALENDARIO -->
		<section id="calendario" class="block">
			<h2>Calendario de Eventos</h2>

			<div class="calendar">
				{#each eventos as e}
					<div class="calendar-card">
						<span class="calendar-date">{formatDate(e.date)}</span>
						<h4>{e.title}</h4>
						<span class="badge examen">Examen</span>
					</div>
				{/each}
			</div>
		</section>

		<!-- ANUNCIOS DESTACADOS -->
		<section id="destacados" class="block highlight">
			<h2>Últimos anuncios</h2>

			{#each anuncios.filter(a => a.important) as a}
				<div class="announcement important">
					<h4>{a.title}</h4>
					<span>{formatDate(a.date)}</span>
					<p>{a.content}</p>
				</div>
			{/each}
		</section>

		<!-- TODOS LOS ANUNCIOS -->
		<section id="todos" class="block">
			<h2>Todos los anuncios</h2>

			{#each anuncios as a}
				<div class="announcement">
					<h4>{a.title}</h4>
					<span>{formatDate(a.date)}</span>
					<p>{a.content}</p>
				</div>
			{/each}
		</section>

	</div>
</section>

<style>
.page {
	display: grid;
	grid-template-columns: 200px 1fr;
	max-width: 1300px;
	margin: auto;
	padding: 2rem 1rem;
	gap: 2rem;
	background: #ffffff;
}

/* Navegación */
.side-nav {
	position: sticky;
	top: 2rem;
	display: flex;
	flex-direction: column;
	gap: 1rem;
}

.side-nav a {
	text-decoration: none;
	color: #003a8f;
	font-weight: 600;
	background: #f4f7fb;
	padding: 0.6rem 0.8rem;
	border-radius: 8px;
}

/* Bloques */
.block {
	margin-bottom: 3rem;
}

.block h2 {
	color: #003a8f;
	margin-bottom: 1.5rem;
}

/* Calendario */
.calendar {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
	gap: 1.5rem;
}

.calendar-card {
	background: #f9fbff;
	padding: 1.5rem;
	border-radius: 16px;
	box-shadow: 0 10px 25px rgba(0,0,0,0.07);
}

.calendar-date {
	font-size: 0.85rem;
	color: #555;
}

.badge {
	display: inline-block;
	margin-top: 0.5rem;
	padding: 0.2rem 0.6rem;
	border-radius: 999px;
	font-size: 0.75rem;
}

.examen {
	background: #003a8f;
	color: white;
}

/* Anuncios */
.highlight {
	background: #fff5f6;
	padding: 2rem;
	border-radius: 20px;
}

.announcement {
	background: #ffffff;
	padding: 1.5rem;
	border-radius: 14px;
	box-shadow: 0 8px 20px rgba(0,0,0,0.05);
	margin-bottom: 1.5rem;
}

.announcement.important {
	border-left: 6px solid #b00020;
}

.announcement span {
	font-size: 0.8rem;
	color: #666;
}
</style>
