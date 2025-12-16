<section class="page-header">
	<h1>Recursos de Apoyo</h1>
	<p>
		Canales oficiales de comunicación para postulantes a la FCyT – UMSS
	</p>
</section>

<section class="resources-section">

	<div class="resources-grid">

		<!-- TELEGRAM -->
		<div class="resource-card telegram">
			<div class="icon">✈️</div>
			<h3>Telegram</h3>

			<img
				src="https://api.qrserver.com/v1/create-qr-code/?size=140x140&data=https://t.me/fcyt_umss"
				alt="QR Telegram FCyT"
			/>

			<a
				href="https://t.me/fcyt_umss"
				target="_blank"
				rel="noopener"
				class="btn"
			>
				Abrir
			</a>
		</div>

		<!-- WHATSAPP -->
		<div class="resource-card whatsapp">
			<div class="icon">💬</div>
			<h3>WhatsApp</h3>

			<img
				src="https://api.qrserver.com/v1/create-qr-code/?size=140x140&data=https://whatsapp.com/channel/0029Vae7Oov0wajtTjMSnj1v"
				alt="QR WhatsApp FCyT"
			/>

			<a
				href="https://whatsapp.com/channel/0029Vae7Oov0wajtTjMSnj1v"
				target="_blank"
				rel="noopener"
				class="btn"
			>
				Abrir
			</a>
		</div>

		<!-- FACEBOOK -->
		<div class="resource-card facebook">
			<div class="icon">📘</div>
			<h3>Facebook</h3>

			<img
				src="https://api.qrserver.com/v1/create-qr-code/?size=140x140&data=https://www.facebook.com/umss.fcyt"
				alt="QR Facebook FCyT"
			/>

			<a
				href="https://www.facebook.com/umss.fcyt"
				target="_blank"
				rel="noopener"
				class="btn"
			>
				Abrir
			</a>
		</div>

	</div>
</section>

<style>
/* ---------- HEADER ---------- */

.page-header {
	max-width: 1100px;
	margin: 0 auto 2.5rem;
	padding: 2.5rem 1rem 1.5rem;
	text-align: center;
}

.page-header h1 {
	font-size: clamp(2rem, 4vw, 2.6rem);
	color: #003a8f;
	margin-bottom: 0.6rem;
	position: relative;
}

.page-header h1::after {
	content: "";
	display: block;
	width: 80px;
	height: 4px;
	background: linear-gradient(90deg, #003a8f, #b00020);
	margin: 0.8rem auto 0;
	border-radius: 99px;
}

.page-header p {
	color: #555;
	font-size: 1.05rem;
	max-width: 600px;
	margin: 0.8rem auto 0;
}

/* ---------- RESOURCES ---------- */

.resources-section {
	max-width: 1100px;
	margin: 0 auto;
	padding: 0 1rem 3rem;
}

.resources-grid {
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	gap: 1.8rem;
}

/* CARD */
.resource-card {
	background: white;
	border-radius: 18px;
	padding: 1.6rem 1.2rem;
	text-align: center;
	box-shadow: 0 10px 25px rgba(0,0,0,0.08);
	transition: transform .25s ease, box-shadow .25s ease;
}

.resource-card:hover {
	transform: translateY(-6px);
	box-shadow: 0 18px 40px rgba(0,0,0,0.12);
}

.resource-card h3 {
	margin-bottom: 0.6rem;
}

.resource-card img {
	margin: 0.8rem auto 1rem;
	border-radius: 12px;
	background: white;
	padding: 0.4rem;
}

/* ICON */
.icon {
	font-size: 1.8rem;
	margin-bottom: 0.4rem;
}

/* BUTTON */
.btn {
	display: inline-block;
	padding: 0.45rem 1.2rem;
	border-radius: 999px;
	color: white;
	font-size: 0.9rem;
	font-weight: 600;
	text-decoration: none;
}

/* COLORS */
.telegram {
	border-top: 5px solid #229ed9;
}
.telegram .btn {
	background: #229ed9;
}

.whatsapp {
	border-top: 5px solid #25d366;
}
.whatsapp .btn {
	background: #25d366;
}

.facebook {
	border-top: 5px solid #1877f2;
}
.facebook .btn {
	background: #1877f2;
}

/* ---------- RESPONSIVE ---------- */

@media (max-width: 900px) {
	.resources-grid {
		grid-template-columns: repeat(2, 1fr);
	}
}

@media (max-width: 600px) {
	.resources-grid {
		grid-template-columns: 1fr;
	}

	.resource-card img {
		width: 150px;
		height: 150px;
	}
}
</style>
