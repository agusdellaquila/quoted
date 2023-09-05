<script>
	import { onMount } from 'svelte';

	let services = [
		{
			id: 1,
			name: "Sitio Web Clásico",
			details: [
			"Puede contener hasta 5 páginas de contenido.",
			"Iinformación de contacto en el sitio.",
			"Diseño completamente responsive para adaptarse a dispositivos móviles y de escritorio.",
			],
			price: 200,
			type: "Fijo",
		},
		{
			id: 2,
			name: "Optimización SEO",
			details: [
			"Optimización SEO con optimización de palabras clave relevantes para mejorar el ranking en Google.",
			"Estrategias para mejorar la visibilidad en los motores de búsqueda.",
			],
			price: 25,
			type: "Fijo",
		},
		{
			id: 3,
			name: "Documento de Identidad de Marca",
			details: [
			"Creación de un documento de identidad de marca completo.",
			"Contará con una guía de estilo para tu marca: incluidos logotipos; fuentes y paletas de colores.",
			],
			price: 30,
			type: "Fijo",
		},
		{
			id: 4,
			name: "Diseño de Logo",
			details: [
			"Creación de un logotipo único y atractivo para tu empresa o marca.",
			"Se explorarán diversas opciones de diseño y se realizarán revisiones hasta que estés satisfecho con el resultado final.",
			],
			price: 75,
			type: "Fijo",
		},
		{
			id: 5,
			name: "Imagen Corporativa",
			details: [
			"Asesoramiento en la adquisición de un dominio personal (www) para tu empresa.",
			"Creación de correos electrónicos corporativos personalizados (Ejemplo: info@tu-negocio.com).",
			],
			price: 20,
			type: "Fijo",
		},
		{
			id: 6,
			name: "Creación y lanzado de redes sociales",
			details: [
			"La creación de redes implica la inicialización de tus perfiles en redes sociales.",
			"Carga de catálogo de productos o servicios.",
			"Se crearán historias de contacto atractivas con información de contacto; métodos de pago & envío y promoción de tus productos o servicios.",
			],
			price: 150,
			type: "Fijo",
		},
		{
			id: 7,
			name: "Creación de contenido",
			details: [
			"Este servicio proporciona contenido mensual para tus perfiles de redes sociales.",
			"El contenido será atractivo y relevante para tu audiencia.",
			"Puedes personalizar el tipo de contenido que se creará.",
			],
			price: 100,
			type: "Mensual",
		},
		{
			id: 8,
			name: "Hosting",
			details: [
			"El servicio de hosting incluye alojamiento para tu sitio web y que quede disponible en línea.",
			],
			price: 8,
			type: "Mensual",
		},
		{
			id: 9,
			name: "Páginas extras",
			details: [
			"Este servicio te permite agregar páginas adicionales a tu sitio web.",
			],
			price: 20,
			type: "Fijo",
		},
		{
			id: 10,
			name: "Mantenimiento del sitio",
			details: [
			"Soporte continuo y mantenimiento para realizar cambios y actualizaciones en tu sitio web durante el mes.",
			"Tu sitio estará actualizado y funcionando sin problemas.",
			],
			price: 55,
			type: "Fijo",
		},
		{
			id: 11,
			name: "Ecommerce",
			details: [
			"Agregar funcionalidad ecommerce a tu sitio web para que puedas vender productos en línea.",
			"Esto incluye la configuración de carros de compra y pasarelas de pago.",
			],
			price: 250,
			type: "Fijo",
		},
		{
			id: 12,
			name: "Subida de productos",
			details: [
			"Nosotros cargaremos manualmente todos tus productos a tu tienda en línea.",
			"Esto incluye desde imágenes a descripciones y precios.",
			"El precio es calculado según cantidad de productos (5usd x cada 10 productos)",
			],
			price: 5,
			type: "c/10 Productos",
		},
		{
			id: 13,
			name: "CMS",
			details: [
			"Agregar funcionalidad CMS (Sistema de Gestión de Contenido) a tu sitio web para que vos puedas editar y publicar contenido sin la necesidad de un programador.",
			],
			price: 150,
			type: "Fijo",
		},
		{
			id: 14,
			name: "Sistema de turnos",
			details: [
			"Con este servicio podrás ofrecer la programación de citas en línea para tus clientes.",
			"Usamos la solución de agendaPro para gestionar los turnos; la cual tiene su coste mensual.",
			],
			price: 35,
			type: "Fijo",
		},
		{
			id: 15,
			name: "Sistema de gestión Stocky",
			details: [
			"Este servicio proporciona un sistema de gestión completo para tu empresa donde podrá gestionar clientes; productos; pedidos; facturas y más.",
			"Incluye características como seguimiento de inventario.",
			],
			price: 500,
			type: "Fijo",
		},
		{
			id: 16,
			name: "Mantenimiento mensual de Stocky",
			details: [
			"El mantenimiento de Stocky te ayuda con soporte para mantener tus tablas y registros organizados y actualizados con nuestra ayuda",
			],
			price: 60,
			type: "Mensual",
		},
	];
	let selectedServices = [];
	let clientName = '';
	let projectTitle = 'Proyecto Web';
	let monthlyTitle = 'Mantenimiento Mensual';
	let totalFijo = 0;
	let totalMensual = 0;

	// Get the current date
	const currentDate = new Date();

	// Define formatting options
	const options = { year: 'numeric', month: 'long', day: 'numeric' };

	// Format the date as a string
	const formattedDate = currentDate.toLocaleDateString('en-US', options);

	function printDiv(divName) {
		var printContents = document.getElementById(divName).innerHTML;
		var originalContents = document.body.innerHTML;

		document.body.innerHTML = printContents;

		window.print();

		document.body.innerHTML = originalContents;
	}
  
	onMount(() => {
		// Este código se ejecutará después de que el componente se monte en el lado del cliente
		const checkboxes = document.querySelectorAll('input[type="checkbox"]');

		checkboxes.forEach(checkbox => {
			checkbox.addEventListener('change', (event) => {
				let deets = event.target.dataset.details;
				deets = deets.split(',');
				const serviceName = event.target.dataset.name;
				const serviceIncludes = deets;
				const servicePrice = event.target.dataset.price;
				const serviceType = event.target.dataset.type;

				if (event.target.checked) {
					// Agregar el servicio a la lista de seleccionados
					selectedServices = [...selectedServices, { name: serviceName, details: serviceIncludes, price: servicePrice, type: serviceType }];
					console.log(selectedServices);
					if (serviceType === 'Fijo') {
						totalFijo += parseInt(servicePrice);
					} else {
						totalMensual += parseInt(servicePrice);
					}
				} else {
					// Eliminar el servicio de la lista de seleccionados
					selectedServices = selectedServices.filter(service => service.name !== serviceName);
					if (serviceType === 'Fijo') {
						totalFijo -= parseInt(servicePrice);
					} else {
						totalMensual -= parseInt(servicePrice);
					}
				}
			});
		});
	});
</script>


<svelte:head>
	<title>Servicios</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<body>
	<div class="data-container-child overflow-x-hidden">
		<div class="inline-block width-table shadow rounded-lg overflow-x-auto mx-4 lg:mx-0">
			<table class="min-w-full leading-normal">
				<thead>
					<tr>
						<th class="px-2 py-3 border-b border-gray-200 text-gray-800 text-sm font-semibold bg-table-titles">Tick</th>
						<th class="px-2 py-3 border-b border-gray-200 text-gray-800 text-sm font-semibold bg-table-titles">Servicio</th>
						<th class="px-2 py-3 border-b border-gray-200 text-gray-800 text-sm font-semibold bg-table-titles">Precio</th>
						<th class="px-2 py-3 border-b border-gray-200 text-gray-800 text-sm font-semibold bg-table-titles">Tipo</th>
					</tr>
				</thead>
				<tbody>
					{#each services as service}
						<tr class='bg-white even:bg-gray-50'>
							<td class="px-2 py-2 text-sm">
								<label class="container">
									<input type="checkbox" data-name={service.name} data-details={service.details} data-price={service.price} data-type={service.type}>
									<div class="checkmark"></div>
								</label>
							</td>
							<td class="px-2 py-2 text-sm">{service.name}</td>
							<td class="px-2 py-2 text-sm">{service.price} usd</td>
							<td class={`px-2 py-2 text-sm text-center font-semibold ${service.type === 'Fijo' ? 'text-green-600' : service.type === 'Mensual' ? 'text-blue-600' : ' text-purple-600'}`}>{service.type}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</div>

	{#if selectedServices && selectedServices.length > 0}
		<div class="mt-20 bg-white shadow-md rounded-md w-11/12 p-4">
			<h2 class="text-xl font-semibold mt-4 text-center mb-10">Personaliza el presupuesto</h2>
			
			<div class="flex flex-col md:flex-row gap-10 justify-evenly">
				<div class="coolinput">
					<label for="input" class="text">Client Name</label>
					<input type="text" name="input" class="input" bind:value={clientName}>
				</div>
		
				<div class="coolinput">
					<label for="input" class="text">Project Title</label>
					<input type="text" name="input" class="input" bind:value={projectTitle}>
				</div>
		
				<div class="coolinput">
					<label for="input" class="text">Monthly Title</label>
					<input type="text" name="input" class="input" bind:value={monthlyTitle}>
				</div>
			</div>
		</div>

		<div id="printableArea" class="w-11/12 mt-20">
			<div class="flex justify-between bg-indigo-300 p-6">
				<div>{clientName}</div>
				<div>{formattedDate}</div>
			</div>

			<div class="bg-white p-6">
				{#if totalFijo > 0}
					<h2 class="text-xl font-semibold">{projectTitle} $ {totalFijo}</h2>
					
					{#if selectedServices.length > 0}
						{#each selectedServices as service}
							{#if service.type === 'Fijo'}
								<div class="p-4 m-4 rounded-lg">
									<h3 class="text-lg font-semibold">{service.name}</h3>
									<ol type="i" class="pl-4 text-sm">
										{#each service.details as detail}
											<li>{detail}</li>
										{/each}
									</ol>
								</div>
							{/if}
						{/each}
					{/if}
				{/if}

				{#if totalMensual > 0}
					<h2 class="text-xl font-semibold">{monthlyTitle} $ {totalMensual}</h2>

					{#if selectedServices.length > 0}
						{#each selectedServices as service}
							{#if service.type === 'Mensual'}
								<div class="p-4 m-4 rounded-lg">
									<h3 class="text-lg font-semibold">{service.name}</h3>
									<ol type="i" class="pl-4 text-sm">
										{#each service.details as detail}
											<li>{detail}</li>
										{/each}
									</ol>
								</div>
							{/if}
						{/each}
					{/if}
				{/if}
			</div>
		</div>	

		<button on:click={() => {printDiv('printableArea')}} class="cssbuttons-io-button mt-10">
			<svg height="24" width="24" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M0 0h24v24H0z" fill="none"></path><path d="M1 14.5a6.496 6.496 0 0 1 3.064-5.519 8.001 8.001 0 0 1 15.872 0 6.5 6.5 0 0 1-2.936 12L7 21c-3.356-.274-6-3.078-6-6.5zm15.848 4.487a4.5 4.5 0 0 0 2.03-8.309l-.807-.503-.12-.942a6.001 6.001 0 0 0-11.903 0l-.12.942-.805.503a4.5 4.5 0 0 0 2.029 8.309l.173.013h9.35l.173-.013zM13 12h3l-4 5-4-5h3V8h2v4z" fill="currentColor"></path></svg>
			<span>Descargar PDF</span>
	  	</button>
	{/if}
</body>


<style>
	.data-container {
    margin-left: 0;
    width: 100vw;
	}
	.data-container-child {
		margin-left: 0;
		width: 100vw;
	}

	ol {list-style-type: lower-roman;}

	.cssbuttons-io-button {
		display: flex;
		align-items: center;
		font-family: inherit;
		font-weight: 500;
		font-size: 17px;
		padding: 0.8em 1.5em 0.8em 1.2em;
		color: white;
		background: #ad5389;
		background: linear-gradient(0deg, rgba(77,54,208,1) 0%, rgba(132,116,254,1) 100%);
		border: none;
		box-shadow: 0 0.7em 1.5em -0.5em #4d36d0be;
		letter-spacing: 0.05em;
		border-radius: 20em;
	}

	.cssbuttons-io-button svg {
		margin-right: 8px;
	}

	.cssbuttons-io-button:hover {
		box-shadow: 0 0.5em 1.5em -0.5em #4d36d0be;
	}

	.cssbuttons-io-button:active {
		box-shadow: 0 0.3em 1em -0.5em #4d36d0be;
	}


	/* Hide the default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.container {
  display: flex;
  gap: 10px;
}


/* Create a custom checkbox */
.checkmark {
  position: relative;
  box-shadow: rgb(255, 84, 0) 0px 0px 0px 2px;
  height: 20px;
  width: 20px;
  margin-right: 10px;
  flex-shrink: 0;
  margin-top: -1px;
  transition: all 0.2s ease 0s;
  cursor: pointer;
  transform-origin: 0px 10px;
  border-radius: 4px;
  margin: -1px 10px 0px 0px;
  padding: 0px;
  box-sizing: border-box;
}

.container input:checked ~ .checkmark {
  box-shadow: rgb(255, 84, 0) 0px 0px 0px 2px;
  background-color: rgba(245, 24, 24, 0.5);
  height: 20px;
  width: 20px;
  margin-right: 10px;
  flex-shrink: 0;
  margin-top: -1px;
  transition: all 0.2s ease 0s;
  cursor: pointer;
  transform-origin: 0px 10px;
  border-radius: 4px;
  margin: -1px 10px 0px 0px;
  padding: 0px;
  box-sizing: border-box;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 0.45em;
  top: 0.25em;
  width: 0.25em;
  height: 0.5em;
  border: solid white;
  border-width: 0 0.15em 0.15em 0;
  transform: rotate(45deg);
  transition: all 500ms ease-in-out;
}



.coolinput {
  display: flex;
  flex-direction: column;
  width: fit-content;
  position: static;
  max-width: 240px;
}

.coolinput label.text {
  font-size: 0.75rem;
  color: #818CF8;
  font-weight: 700;
  position: relative;
  top: -0.1rem;
  margin: 0 0 0 7px;
  padding: 0 3px;
  background: #818df839;
  border-radius: 5px;
  width: fit-content;
}

.coolinput input[type=text].input {
  padding: 11px 10px;
  font-size: 0.75rem;
  border: 2px #818CF8 solid;
  border-radius: 5px;
}

.coolinput input[type=text].input:focus {
  outline: none;
}
</style>
