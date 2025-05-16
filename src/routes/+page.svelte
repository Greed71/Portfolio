<script lang="ts">
	import { onMount } from 'svelte';

	let cards: HTMLDivElement;
	let interval: ReturnType<typeof setInterval>;

	onMount(() => {
		interval = setInterval(() => {
			if (cards && cards.children.length > 0) {
				const first = cards.children[0] as HTMLDivElement;
				first.style.transition = 'margin-left 0.4s';
				first.style.marginLeft = '-320px'; // larghezza card + gap
				setTimeout(() => {
					first.style.transition = 'none';
					first.style.marginLeft = '';
					cards.appendChild(first);
					// Forza il reflow per il browser
					void first.offsetWidth;
				}, 400); // deve essere uguale alla durata della transizione CSS
			}
		}, 2000);

		return () => clearInterval(interval);
	});
</script>

<div class="container funnel-sans-regular">
    <div class="top-icons">
        <a href="/english" aria-label="English" title="English">
            <img src="/gb.png" alt="English Flag" class="flag" width="32" height="32" />
        </a>
    </div>
	<div class="block-grad block">
		<h1>Salve, il mio nome è Mariano L.</h1>
        <h2>Sono un laureato in Informatica, appassionato di sviluppo software e di tutto ciò che riguarda il mondo tech.</h2>
        <div class="block-links">
            <a href="https://www.linkedin.com/in/marianolongo" class="block-link" target="_blank" rel="noopener">
                <img src="/linkedin.png" alt="linkedin" width="32" height="32" /></a>
            <a href="https://github.com/Greed71" class="block-link" target="_blank" rel="noopener">
                <img src="/git.png" alt="Git" width="32" height="32" /></a>
        </div>
	</div>
	<div class="cards" bind:this={cards}>
		<div class="card card-rosso">Contenuto 1</div>
		<div class="card card-blu">Contenuto 2</div>
		<div class="card card-giallo">Contenuto 3</div>
		<div class="card card-verde">Contenuto 4</div>
		<div class="card card-viola">Contenuto 5</div>
		<!-- Aggiungi altri quadrettoni qui -->
	</div>
    <div class="footer-link">
        <a href="https://github.com/Greed71/Portfolio" aria-label="Git">
            <img src="/git.png" alt="GitHub Logo" class="github-logo" width="32" height="32" />
            Visualizza il codice sorgente su GitHub
        </a>
    </div>
</div>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        min-height: 100vh;
        background-color: #006d5b; 
        font-family: sans-serif;
    }

    h1 {
        font-size: 2rem;
        font-weight: 700;
        margin: 0;
        padding: 0;
    }

    h2 {
        text-align: left;
        font-size: 1.4rem;
        font-weight: 400;
        margin: 0;
        padding: 0;
    }

    .container {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: flex-end; 
        justify-content: center; 
        color: white;
        position: relative;
        z-index: 1;
    }

    .block {
        width: 100%;
        min-height: 300px;
        max-width: 1000px;
        background: rgba(255, 255, 255, 0.1);
        border-radius: 1rem;
        box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
        padding: 2rem;
        color: white;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
        text-align: center;
        font-size: 1.5rem;
        margin-top: 0;
        margin-bottom: 2rem;
        position: relative;
    }

    .block-link {
        margin-top: auto;
        margin-bottom: 0;
        align-self: center;
        color: #fff;
        padding: 0.5rem 0.2rem; /* padding orizzontale ridotto */
        text-decoration: none;
        font-weight: bold;
    }

    .block-links {
        display: flex;
        gap: 0rem;         /* nessuno spazio tra i link */
        margin-top: auto;
        margin-bottom: 0;
        justify-content: center;
        width: 100%;
    }

    .cards {
        display: flex;
        gap: 2rem;
        overflow: hidden;
        width: 100%;
        max-width: 1000px;
        margin-top: 0;
        flex-wrap: nowrap;
        justify-content: flex-start;
        position: relative;
        padding-top: 12px;
        padding-bottom: 12px;
        padding-right: 18px;
        padding-left: 18px;
    }

    .card {
        background: rgba(255, 255, 255, 0.1);
        border-radius: 1rem;
        box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
        padding: 2rem;
        min-width: 300px;
        min-height: 180px;
        max-width: 300px;
        color: white;
        display: flex;
        align-items: flex-start;  
        justify-content: flex-start;  
        text-align: left;             
        font-size: 1.2rem;
        transition: margin-left 0.4s;
        flex-shrink: 0;
    }

    .block-grad {
        background: linear-gradient(135deg, #3498db 0%, #9b59b6 100%);
    }

    .card-rosso {
        background: #e74c3c;
    }
    .card-blu {
        background: #4e44db;
    }
    .card-giallo {
        background: #f1c40f;
    }
    .card-verde {
        background: #2ecc71;
    }
    .card-viola {
        background: #9b59b6;
    }

    .funnel-sans-regular {
        font-family: "Funnel Sans", sans-serif;
        font-optical-sizing: auto;
        font-weight: 300;
        font-style: normal;
    }

    .top-icons {
        width: 100%;
        max-width: 1000px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        margin-bottom: 0; 
        gap: 0.5rem;
    }

    .flag {
        font-size: 2rem;
        user-select: none;
    }

    .footer-link {
        width: 100%;
        position: fixed;
        bottom: 20px;
        left: 0;
        display: flex;
        justify-content: center;
        z-index: 10;
    }

    .footer-link a {
        color: rgb(0, 0, 0);
        text-decoration: none;
        font-size: 1rem;
        font-weight: bold;
        display: inline-flex;
        align-items: center;
        gap: 0.5rem;
    }
</style>
