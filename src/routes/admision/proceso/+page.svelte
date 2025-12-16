<script>
	let modo = "PSA";
	let descargado = false;

	function descargarChecklist() {
		const archivo = modo === "PSA" ? "/check/PSA.jpg" : "/check/CPU.jpg";

		const link = document.createElement("a");
		link.href = archivo;
		link.download = `checklist-${modo}.jpg`;
		link.click();

		descargado = true;
	}
</script>

<section class="page">

	<!-- MENÚ LATERAL (SOLO DESKTOP) -->
	<nav class="side-nav">
		<a href="#fechas">📅 Fechas</a>
		<a href="#opciones">📝 Opciones</a>
		<a href="#cpu">🎓 CPU</a>
		<a href="#cronograma">🗂 Cronograma</a>
		<a href="#requisitos">✅ Requisitos</a>
		<a href="#info">ℹ Información</a>
		<a href="#ayuda">🆘 Ayuda</a>
	</nav>

	<!-- CONTENIDO -->
	<main class="content">

		<section id="fechas" class="block highlight blue">
			<h2>Fechas del Examen de Ingreso (PSA)</h2>

			<div class="cards">
				<div class="card red">
					<h4>Primera Opción</h4>
					<p>Viernes 16 de enero de 2026</p>
					
				</div>
				<div class="card red">
					<h4>Segunda Opción</h4>
					<p>Lunes 2 de febrero de 2026</p>
				</div>
				<div class="card red">
					<h4>Tercera Opción</h4>
					<p>Jueves 12 de febrero de 2026</p>
				</div>
			</div>
		</section>

		<section id="opciones" class="block">
			<h2>Opciones de Postulación</h2>

			<div class="cards">
				<div class="card">
					<h4>Primera Opción</h4>
					<p class="price">Bs 600</p>
					<small>Bs 300 si reprobó CPU 2-2025</small>
				</div>
				<div class="card">
					<h4>Segunda Opción</h4>
					<p class="price">Bs 600</p>
				</div>
				<div class="card">
					<h4>Tercera Opción</h4>
					<p class="price">Bs 600</p>
				</div>
			</div>
		</section>

		<section id="cpu" class="block highlight yellow">
			<h2>Curso Preuniversitario (CPU)</h2>
			<p><strong>Duración:</strong> 4 de noviembre al 30 de diciembre de 2025</p>
			<p><strong>Costo:</strong> Bs 1000</p>
			<p><strong>Modalidad:</strong> Virtual con evaluaciones presenciales</p>
		</section>

		<section id="cronograma" class="block">
			<h2>Cronograma del Proceso</h2>

			<div class="toggle">
				<button class:active={modo==="PSA"} on:click={() => {modo="PSA"; descargado=false}}>PSA</button>
				<button class:active={modo==="CPU"} on:click={() => {modo="CPU"; descargado=false}}>CPU</button>
			</div>

			<ul class="timeline">
				{#if modo === "PSA"}
					<li>Registro y llenado de formulario</li>
					<li>Pago del derecho al examen</li>
					<li>Examen presencial</li>
					<li>Publicación de resultados</li>
				{:else}
					<li>Inscripción al curso</li>
					<li>Pago del CPU</li>
					<li>Clases virtuales</li>
					<li>Evaluaciones presenciales</li>
				{/if}
			</ul>
		</section>

		<section id="requisitos" class="block highlight green">
			<h2>Checklist de Requisitos</h2>

			<div class="toggle">
				<button class:active={modo==="PSA"} on:click={() => {modo="PSA"; descargado=false}}>PSA</button>
				<button class:active={modo==="CPU"} on:click={() => {modo="CPU"; descargado=false}}>CPU</button>
			</div>

			<ul class="checklist">
				{#if modo === "PSA"}
					<li>Formulario de inscripción impreso</li>
					<li>Cédula de identidad vigente</li>
					<li>Comprobante de pago</li>
					<li>Fotografía digital válida</li>
				{:else}
					<li>Formulario de inscripción al CPU</li>
					<li>Cédula de identidad vigente</li>
					<li>Comprobante de pago</li>
					<li>Correo electrónico activo</li>
				{/if}
			</ul>

			<button
				class="download"
				class:done={descargado}
				on:click={descargarChecklist}>
				{descargado ? "✔ Checklist descargado" : "⬇ Descargar checklist"}
			</button>
		</section>

		<section id="info" class="block">
			<h2>Información del Examen PSA</h2>
			<p><strong>Lugar:</strong> Edificio Académico 2 – FCyT</p>
			<p><strong>Asignaturas:</strong> Aritmética, Geometría, Física, Química y Biología</p>
			<p><strong>Nota mínima:</strong> 51 puntos</p>
		</section>

		<section id="ayuda" class="block highlight blue help">
			<h2>¿Necesitas ayuda?</h2>
			<p>
				Consulta las guías paso a paso, instructivos oficiales y tutoriales
				para completar correctamente tu proceso de admisión.
			</p>

			<a href="/admision/tutoriales" class="help-btn">
				Ir a Guías y Tutoriales
			</a>
		</section>

	</main>
</section>

<style>
.page {
	display: grid;
	grid-template-columns: 220px 1fr;
	gap: 2rem;
	max-width: 1300px;
	margin: auto;
	padding: 1.5rem;
}

/* OCULTAR MENÚ EN MÓVIL */
@media (max-width: 900px) {
	.page {
		grid-template-columns: 1fr;
	}
	.side-nav {
		display: none;
	}
}

/* MENÚ */
.side-nav {
	display: flex;
	flex-direction: column;
	gap: 0.6rem;
	position: sticky;
	top: 1rem;
}

.side-nav a {
	padding: 0.6rem;
	border-radius: 12px;
	background: #eef4ff;
	color: #003a8f;
	font-weight: 600;
	text-decoration: none;
}

/* BLOQUES */
.block {
	margin-bottom: 3rem;
}

.highlight {
	padding: 2rem;
	border-radius: 20px;
}

.blue { background: #f4f8ff; }
.yellow { background: #fff8e6; }
.green { background: #f1fbf4; }

/* CARDS */
.cards {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
	gap: 1.5rem;
}

.card {
	background: white;
	padding: 1.5rem;
	border-radius: 16px;
	box-shadow: 0 10px 25px rgba(0,0,0,0.08);
}

.card.red {
	border-left: 6px solid #b00020;
}

.price {
	font-size: 1.4rem;
	font-weight: bold;
	color: #003a8f;
}

/* TOGGLE */
.toggle button {
	margin-right: 0.6rem;
	padding: 0.4rem 1rem;
	border-radius: 999px;
	border: none;
	background: #ddd;
	cursor: pointer;
}

.toggle .active {
	background: #003a8f;
	color: white;
}

/* CHECKLIST */
.checklist {
	margin: 1.5rem 0;
	padding-left: 1.2rem;
}

/* BOTÓN */
.download {
	padding: 0.7rem 1.5rem;
	border-radius: 999px;
	border: none;
	background: #16a34a;
	color: white;
	font-weight: 600;
	cursor: pointer;
}

.download.done {
	background: #0f766e;
}

/* AYUDA */
.help {
	text-align: center;
}

.help-btn {
	display: inline-block;
	margin-top: 1rem;
	padding: 0.8rem 1.6rem;
	border-radius: 999px;
	background: #003a8f;
	color: white;
	font-weight: 600;
	text-decoration: none;
}
</style>
