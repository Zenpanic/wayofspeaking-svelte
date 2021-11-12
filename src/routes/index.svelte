<script>
	import validator from 'validator';
	import DOMPurify from 'dompurify';

	let email = '';
	let message = '';
	let phone = '';

	$: emailOk = email && validator.isEmail(email);
	$: messageOk = message && message.length > 5;
	$: formOk = emailOk && messageOk;

	let loading = false;
	let messageSent = false;

	const sendMessage = async () => {
		if (!formOk || phone) return;
		loading = true;
		let cleanMessage = DOMPurify.sanitize(message);
		let cleanEmail = DOMPurify.sanitize(email);
		messageSent = false;
		const res = await fetch('/api/formHandler', {
			method: 'POST',
			credentials: 'include',
			headers: { 'Content-type': 'application/json;charset=UTF-8' },
			body: JSON.stringify({
				email: cleanEmail,
				message: cleanMessage
			})
		});
		const data = await res.json();
		if (data.message) loading = false;
		if (data.message === 'ok') messageSent = true;
		message = '';
		email = '';
		return;
	};
</script>

<header
	id=" header-part"
	class="vh-100 dt w-100 tc bg-dark-gray white cover top-page"
	style="background:url(/images/background-opt.jpg) no-repeat center;"
>
	<div class="dtc v-mid">
		<h1 class="animate__animated animate__fadeInUp f1 f-headline-l fw1 i white-60">
			Way Of Speaking
		</h1>
		<blockquote class="ph0 mh0 measure f4 lh-copy center">
			<p class="fw1 white-70">Enseignement d'anglais en ligne</p>
			<cite class="f6 ttu fw8 tracked fs-normal">Via Skype et Google Meet</cite>
		</blockquote>
	</div>
</header>

<nav class="tc mw7 center mt0">
	<a
		class="f6 f5-l link bg-animate black-80 hover-bg-light-yellow dib pa3 ph4-l"
		href="#header-part">Accueil</a
	>
	<a class="f6 f5-l link bg-animate black-80 hover-bg-light-red dib pa3 ph4-l" href="#about-me"
		>Mon Parcours</a
	>
	<a
		class="f6 f5-l link bg-animate black-80 hover-bg-light-blue dib pa3 ph4-l"
		href="#approche-pedago">Approche Pédagogique</a
	>
	<a class="f6 f5-l link bg-animate black-80 hover-bg-light-pink dib pa3 ph4-l" href="#contact"
		>Contact</a
	>
</nav>

<article id="about-me" class="cf ph3 ph5-ns pt5 bb">
	<div class="fn fl-ns w-50-ns pr4-ns grow">
		<article class="shadow-2 mw5 center bg-white br3 pa3 pa4-ns mv3 ba b--black-10">
			<div class="tc">
				<img
					src="/images/nina.jpg"
					class="br-100 h4 w4 dib ba b--black-05 pa2"
					title="Nina D"
					alt="Nina D"
				/>
				<h1 class="f3 mb2 light-green">Nina Delgas</h1>
				<h2 class="f5 fw4 light-purple mt0">Enseignante d'anglais</h2>
			</div>
		</article>
	</div>

	<div class="fn fl-ns w-50-ns" style="padding: 1em; box-sizing: border-box;">
		<h2 class="baskerville fw1 ph3 ph0-l">Mon Parcours</h2>
		<p class="measure f5 lh-copy mt0-ns">
			Ayant grandi et vécu en Allemagne, en Australie, aux Caraibes et en Pologne, j'ai toujours été
			entourée par les langues étrangères. Être polyglotte m’a ouvert les portes à des voyages,
			rencontres, formations et études peu banals, qui m'ont aidé à me construire. Après m’être
			installée en Bretagne pour de bon, j’ai continué à me former afin de pouvoir aujourd’hui
			transmettre cette philosophie de bien vivre, sous la forme de cours d’anglais. Je souhaite
			apporter mon aide à ceux qui sont à la recherche de leur identité – les enfants et les
			adolescents.
		</p>
		<p class="measure f5 lh-copy mt0-ns">
			Je dispense des cours d'anglais via webcam auprès de jeunes de 10 à 18 ans depuis 2016. Avant
			cela, j’ai étudié le français à l’Université de Gdansk en Pologne, et j'ai obtenu le diplôme
			TELF qui confirme mes compétences en tant qu’enseignante d’anglais. Je suis également
			professeur certifiée en enseignement de la pensée critique par l’art.
		</p>
		<p class="measure f5 lh-copy mt0-ns">
			A côté de cela, je travaille en tant qu'animatrice périscolaire titulaire du BAFA en école et
			centre de loisirs.
		</p>
	</div>
</article>

<section id="approche-pedago" class="mw7 center avenir">
	<h2 class="baskerville fw1 ph3 ph0-l light-green">Approche Pédagogique</h2>
	<article class="bt bb b--black-10">
		<div class="db pv4 ph3 ph0-l">
			<div class="flex flex-column flex-row-ns">
				<div class="pr3-ns mb4 mb0-ns w-100 w-40-ns">
					<img
						src="/images/illu1.jpg"
						class="shadow-5 appear animate__animated db"
						alt="Cours personnalisés"
					/>
				</div>
				<div class="w-100 w-60-ns pl3-ns">
					<h1 class="f3 fw1 baskerville mt0 lh-title light-purple">Des cours personnalisés</h1>
					<p class="f6 f5-l lh-copy">
						Inspirée par la technique contextuelle d’aprentissage (CLIL) je conçois des cours d’une
						heure selon les thèmes et les objectifs pédagogiques les plus intéressants pour
						l’étudiant, ainsi que son niveau actuel.
					</p>
					<p class="f6 f5-l lh-copy">
						Après une leçon-interview, on décide ensemble quels sont les objectifs ainsi que les
						sujets les plus passionnants pour la personne.
					</p>
				</div>
			</div>
		</div>
	</article>
	<article class="bb b--black-10">
		<div class="db pv4 ph3 ph0-l">
			<div class="flex flex-column flex-row-ns">
				<div class="pr3-ns mb4 mb0-ns w-100 w-40-ns">
					<img
						src="/images/illu2.jpg"
						class="shadow-5 appear db animate__animated"
						alt="Aide scolaire"
					/>
				</div>
				<div class="w-100 w-60-ns pl3-ns">
					<h1 class="f3 fw1 baskerville mt0 lh-title light-purple">L'aide scolaire</h1>
					<p class="f6 f5-l lh-copy">
						En tant qu’animatrice périscolaire je repère bien les difficultés qu’ont les enfants
						avec leurs devoirs et la compréhension du matériel abordé pendant les cours à l’école.
						J’inclue souvent des sujets de programme scolaire dans mes cours personnalisés afin de
						valoriser encore plus les enfants et les adolescents dans leurs progrès.
					</p>
					<p class="f6 f5-l lh-copy">
						L’apprentissage d’une langue étrangère est censée être stimulant et attractif. L’idée
						est que les enfants soient fiers de cette compétence qu’ils développent, et qu'ils
						l'utilisent et la partagent volontiers aussi bien durant le temps scolaire que pendant
						leurs loisirs.
					</p>
				</div>
			</div>
		</div>
	</article>
	<article class="bb b--black-10">
		<div class="db pv4 ph3 ph0-l">
			<div class="flex flex-column flex-row-ns">
				<div class="pr3-ns mb4 mb0-ns w-100 w-40-ns">
					<img
						src="/images/illu3.jpg"
						class="shadow-5 db animate__animated appear"
						alt="Apprendre à réfléchir en anglais"
					/>
				</div>
				<div class="w-100 w-60-ns pl3-ns">
					<h1 class="f3 fw1 baskerville mt0 lh-title light-purple">
						Apprendre à réfléchir en anglais
					</h1>
					<p class="f6 f5-l lh-copy">
						Un des obstacles les plus démotivants qu’on puisse rencontrer sur notre chemin vers le
						bilinguisme est la difficulté de traduire mentalement ce qu’on a à l’esprit.
					</p>
					<p class="f6 f5-l lh-copy">
						Pendant mes cours, on apprend à réflechir en anglais, pour que cela devienne notre
						deuxième language intrapersonnel. Je me base sur le programme pédagogique de
						l’Université de Harvard (Project Zero, Harvard Graduate School of Education), qui permet
						de développer une capacité de réflexion critique et de résolution de problèmes.
					</p>
				</div>
			</div>
		</div>
	</article>
</section>

<section id="contact" class="pv5">
	<div class="pv3 ph3-ns bb tc mw7 center mt0 bb">
		<h2 class="baskerville fw1 ph3 ph0-l">Contact</h2>
		<div class="black-80 form-section" id="message-form">
			<div class="ma1 pa2">
				<label for="email" class="f6 b db mb2">E-mail</label>
				<input
					id="email"
					name="email"
					class="input-reset ba b--black-20 pa2 mb2 db w-100"
					type="email"
					aria-describedby="name-desc"
					bind:value={email}
				/>
				{#if email.length > 0 && !emailOk}
					<small id="name-desc" class="f6 black-60 db mb2"
						>Merci d'entrer une adresse e-mail valide.</small
					>{/if}
				<label class="fancy-field" for="phoneNumberartYUIo">N'écrivez rien ici.</label>
				<input
					name="phoneNumberartYUIo"
					class="fancy-field"
					type="text"
					autocomplete="off"
					bind:value={phone}
				/>
			</div>
			<div class="ma1 pa2">
				<label for="message" class="f6 b db mb2">Message</label>
				<textarea
					id="message"
					name="message"
					class="db border-box hover-black w-100 ba b--black-20 pa2 br2 mb2"
					aria-describedby="comment-desc"
					bind:value={message}
				/>
				<small id="comment-desc" class="f6 black-60"
					>Vous avez une question ?<br />Vous souhaitez un devis ?</small
				>
			</div>
			<div>
				<button
					on:click={sendMessage}
					name="submit-btn"
					class="formButton"
					disabled={!formOk || loading}>Envoyer</button
				>
				{#if messageSent}<p class="okMessage">
						Votre message a bien été envoyé, je vous répondrai sous peu. A bientôt !
					</p>{/if}
			</div>
		</div>
	</div>
</section>

<footer class="pv4 ph3 ph5-m ph6-l mid-gray">
	<small class="f6 db tc"
		>© 2020 - 2021 <b class="ttu">Nina Delgas - ZenTown</b>, All Rights Reserved</small
	>
	<br />
	<small class="f6 db tc"><a class="mentions" href="/legal">Mentions Légales</a></small>
	<div id="legal" />
</footer>

<style>
	.formButton {
		cursor: pointer;
		padding: 0.8em 1.8em;
		background-color: black;
		color: white;
		font-family: monospace;
		font-weight: 600;
		font-size: x-large;
		border: 0px solid black;
		letter-spacing: 0.1em;
	}

	.formButton:disabled {
		cursor: not-allowed;
		color: darkgray;
	}

	.okMessage {
		color: white;
	}
</style>
