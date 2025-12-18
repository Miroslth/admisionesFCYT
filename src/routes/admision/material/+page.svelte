<script>
	import { onMount } from "svelte";

	let selected = null; // 'material' | 'examenes'
	let selectedYear = "Todos";

	// =====================
	// MATERIAL DE ESTUDIO
	// =====================
	const materialEstudio = [
		{ nro: 1, asignatura: "Álgebra - Aritmética", archivo: "algebra-aritmetica.pdf", size: "604 KB" },
		{ nro: 2, asignatura: "Geometría - Trigonometría", archivo: "geometria-trigonometria.pdf", size: "600 KB" },
		{ nro: 3, asignatura: "Química", archivo: "quimica.pdf", size: "474 KB" },
		{ nro: 4, asignatura: "Física", archivo: "fisica.pdf", size: "519 KB" },
		{ nro: 5, asignatura: "Biología", archivo: "biologia.pdf", size: "348 KB" },
		{ nro: 6, asignatura: "Estrategias de Aprendizaje", archivo: "estra-aprendizaje.pdf", size: "—" }
	];

	// =====================
	// EXÁMENES PASADOS
	// =====================
	const examenes = [
		{ year: 2025, title: "Primer Examen de Ingreso FCyT 1-2025", file: "2025-1-1op.pdf", size: "265 KB" },
		{ year: 2025, title: "Segundo Examen de Ingreso FCyT 1-2025", file: "2025-1-2op.pdf", size: "190 KB" },
		{ year: 2025, title: "Tercer Examen de Ingreso FCyT 1-2025", file: "2025-1-3op.pdf", size: "244 KB" },
		{ year: 2025, title: "PREU FCyT 1-2025", file: "2025-1-preu.pdf", size: "1233 KB" },

		{ year: 2024, title: "Primer Examen de Ingreso FCyT 1-2024", file: "2024-1-1op.pdf", size: "232 KB" },
		{ year: 2024, title: "Segundo Examen de Ingreso FCyT 1-2024", file: "2024-1-2op.pdf", size: "154 KB" },
		{ year: 2024, title: "Tercer Examen de Ingreso FCyT 1-2024", file: "2024-1-3op.pdf", size: "289 KB" },
		{ year: 2024, title: "PREU FCyT 1-2024", file: "2024-1-preu.pdf", size: "1286 KB" },

		{ year: 2023, title: "Primer Examen de Ingreso FCyT 1-2023", file: "1-op-1-2023.pdf", size: "244 KB" },
		{ year: 2023, title: "Segundo Examen de Ingreso FCyT 1-2023", file: "2023-2-2op.pdf", size: "331 KB" },

		{ year: 2022, title: "Examen Virtual FCyT 2021–2022", file: "2021-2022virtual.pdf", size: "4.93 MB" },
		{ year: 2020, title: "Primer Examen de Ingreso FCyT 1-2020", file: "161_1ra-op-1-2020.pdf", size: "320 KB" }
	];

	const years = ["Todos", 2025, 2024, 2023, 2022, 2021, 2020];

	$: examenesFiltrados = examenes
		.filter(e => selectedYear === "Todos" || e.year == selectedYear)
		.sort((a, b) => b.year - a.year);

	// =====================
	// HUELLA VISUAL (SOLO SESIÓN)
	// =====================
	let downloaded = new Set();

	onMount(() => {
		const saved = sessionStorage.getItem("downloadedDocs");
		if (saved) {
			downloaded = new Set(JSON.parse(saved));
		}
	});

	function markDownloaded(key) {
	downloaded.add(key);
	downloaded = new Set(downloaded); // fuerza reactividad

	sessionStorage.setItem(
		"downloadedDocs",
		JSON.stringify([...downloaded])
	);
}
</script>


<section class="page">
	<h1>Material de Consulta</h1>
	<p class="subtitle">
		Recursos oficiales para la preparación al proceso de admisión FCyT – UMSS
	</p>

	<!-- CARDS -->
	<div class="cards">
		<button
			class="card blue"
			class:active={selected === 'material'}
			on:click={() => selected = 'material'}
		>
			<div class="icon">📘</div>
			<h2>Material de Estudio</h2>
			<p>Programas analíticos por materia</p>
		</button>

		<button
			class="card red"
			class:active={selected === 'examenes'}
			on:click={() => selected = 'examenes'}
		>
			<div class="icon">📝</div>
			<h2>Exámenes Pasados</h2>
			<p>Exámenes oficiales desde 2020</p>
		</button>
	</div>

	<!-- MATERIAL -->
	{#if selected === 'material'}
	<section class="content">
		<h3>Material de Estudio</h3>

		<table>
			<thead>
				<tr>
					<th>NRO</th>
					<th>ASIGNATURA</th>
					<th>ARCHIVO</th>
					<th>TAMAÑO</th>
					<th>DESCARGAR</th>
				</tr>
			</thead>
			<tbody>
				{#each materialEstudio as m}
				<tr class:seen={downloaded.has(m.archivo)}>
					<td>{m.nro}</td>
					<td>{m.asignatura}</td>
					<td>{m.archivo}</td>
					<td>{m.size}</td>
					<td>
						<a
							href={`/pdfs/${m.archivo}`}
							target="_blank"
							download
							class:done={downloaded.has(m.archivo)}
							on:click={() => markDownloaded(m.archivo)}
						>
							{downloaded.has(m.archivo) ? "Descargado ✓" : "Descargar"}
						</a>
					</td>
				</tr>
				{/each}
			</tbody>
		</table>
	</section>
	{/if}

	<!-- EXÁMENES -->
	{#if selected === 'examenes'}
	<section class="content">
		<h3>Exámenes Pasados</h3>

		<label class="filter">
			Filtrar por año:
			<select bind:value={selectedYear}>
				{#each years as y}
					<option value={y}>{y}</option>
				{/each}
			</select>
		</label>

		<table>
			<thead>
				<tr>
					<th>AÑO</th>
					<th>DESCRIPCIÓN</th>
					<th>ARCHIVO</th>
					<th>TAMAÑO</th>
					<th>DESCARGAR</th>
				</tr>
			</thead>
			<tbody>
				{#each examenesFiltrados as e}
				<tr class:seen={downloaded.has(e.file)}>
					<td>{e.year}</td>
					<td>{e.title}</td>
					<td>{e.file}</td>
					<td>{e.size}</td>
					<td>
						<a
							href={`/pdfs/${e.file}`}
							target="_blank"
							download
							class:done={downloaded.has(e.file)}
							on:click={() => markDownloaded(e.file)}
						>
							{downloaded.has(e.file) ? "Descargado ✓" : "Descargar"}
						</a>
					</td>
				</tr>
				{/each}
			</tbody>
		</table>
	</section>
	{/if}
</section>

<style>
  	.page {
		max-width: 1200px;
		margin: 0 auto;
		padding: 2.5rem 1rem;
		background: white;
	}

	h1 {
		color: #003a8f;
		margin-bottom: 0.3rem;
	}

	.subtitle {
		color: #555;
		margin-bottom: 2rem;
	}

	.cards {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
		margin-bottom: 3rem;
	}

	.card {
		border-radius: 18px;
		padding: 2.5rem 2rem;
		background: white;
		border: 2px solid transparent;
		cursor: pointer;
		text-align: center;
		box-shadow: 0 12px 30px rgba(0,0,0,0.08);
		transition: transform .25s, box-shadow .25s;
	}

	.card:hover {
		transform: translateY(-6px);
		box-shadow: 0 18px 40px rgba(0,0,0,0.12);
	}

	.card.active {
		outline: 3px solid rgba(0,0,0,0.08);
	}

	.card.blue {
		border-color: #3b82f6;
	}

	.card.red {
		border-color: #b00020;
		background: #fff5f6;
	}

	.icon {
		font-size: 3rem;
		margin-bottom: 1rem;
	}

	h2 {
		margin-bottom: 0.5rem;
	}

	.content {
		margin-top: 2rem;
	}

	table {
		width: 100%;
		border-collapse: collapse;
		margin-top: 1rem;
	}

	th, td {
		border: 1px solid #ddd;
		padding: 0.6rem;
	}

	th {
		background: #f5f7fa;
	}

	a {
		color: #b00020;
		font-weight: 600;
		text-decoration: none;
	}

	.filter {
		display: inline-block;
		margin-bottom: 1rem;
	}
  table {
	width: 100%;
	border-collapse: separate;
	border-spacing: 0;
	margin-top: 1.5rem;
	background: white;
	border-radius: 14px;
	overflow: hidden;
	box-shadow: 0 10px 25px rgba(0,0,0,0.06);
	font-size: 0.95rem;
}
thead {
	background: linear-gradient(
		90deg,
		#eaf2ff,
		#f4f8ff
	);
}

th {
	padding: 0.9rem 0.8rem;
	text-align: left;
	color: #003a8f;
	font-weight: 600;
	border-bottom: 1px solid #dbe7ff;
}
tbody tr {
	transition: background 0.2s ease;
}

tbody tr:nth-child(even) {
	background: #fafbff;
}
tbody tr:hover {
	background: #eef4ff;
}
td {
	padding: 0.75rem 0.8rem;
	border-bottom: 1px solid #eee;
	color: #333;
}
td a {
	display: inline-block;
	padding: 0.35rem 0.8rem;
	border-radius: 6px;
	background: #b00020;
	color: white;
	font-size: 0.85rem;
	font-weight: 600;
	text-decoration: none;
	transition: background 0.2s ease, transform 0.2s ease;
}

td a:hover {
	background: #8f0019;
	transform: translateY(-1px);
}
/* Material de estudio */
.content h3 {
	color: #003a8f;
	margin-bottom: 0.5rem;
}

/* Exámenes */
.content:has(select) table thead {
	background: linear-gradient(
		90deg,
		#fff1f3,
		#ffe4e8
	);
}

.content:has(select) th {
	color: #8f0019;
}
	/* SOLO AÑADIDO: huella visual */
	tr.seen {
		background: #f7fbff;
	}

	a.done {
		background: #16a34a !important;
	}
</style>
