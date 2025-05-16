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
        <a href="/" aria-label="Italian" title="Italian">
            <img src="/it.png" alt="Italian Flag" class="flag" width="32" height="32" />
        </a>
    </div>
	<div class="block-grad block">
		<h1>Welcome in my Portfolio!</h1>
	</div>
	<div class="cards" bind:this={cards}>
		<div class="card card-rosso">Contenuto 1</div>
		<div class="card card-blu">Contenuto 2</div>
		<div class="card card-giallo">Contenuto 3</div>
		<div class="card card-verde">Contenuto 4</div>
		<div class="card card-viola">Contenuto 5</div>
		<!-- Aggiungi altri quadrettoni qui -->
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

	.container {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: flex-end; 
		justify-content: center; 
		color: white;
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
		align-items: flex-start;      
		justify-content: center;      
		text-align: center;           
		font-size: 1.5rem;
		margin-top: 0;     
		margin-bottom: 2rem;
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

</style>
