<script>

	// @ts-nocheck
	let files;
	$: if (files) {

		for (const file of files) {
			console.log(`${file.name}: ${file.size} bytes`);

			const reader = new FileReader();
			reader.onload = function(e) {

				// Variables
				const lines = e.target.result.split('\n');
				const result = [];

				// Sanitize the file with regex (� and invalid characters)
				for (let i = 0; i < lines.length; i++) {
					result.push(lines[i].split(';').map((item) => item
					.replace(/[^ -~]/g, '')
					.replace(/�/g, '')
					.replace(/,/g, '')
					.replace(/ +/g, '')
					));

					console.log(result[i]);
				}

				// Sort the array (by order)
				result.sort((a, b) => {
					return a[4] - b[4];
				});

				// Join the array into a string
				const sanitized = result.join('\n').replace(/,/g, ';');

				// Create a new file with the sanitized data
				const blob = new Blob([sanitized], { type: 'text/csv' });
				const url = URL.createObjectURL(blob);
				const a = document.createElement('a');

				// Download the file
				a.setAttribute('hidden', '');
				a.setAttribute('href', url);
				a.setAttribute('download', file.name);
				document.body.appendChild(a);
				a.click();
				document.body.removeChild(a);
				URL.revokeObjectURL(url);
			};
			reader.readAsText(file);
		}

	}
</script>

<label for="many">Drag & drop one or multiple CSV file(s)</label>
<input bind:files id="many" multiple type="file" accept=".csv, .xlsx, .xls"/>

{#if files}
	<h1>Selected files:</h1>
	{#each Array.from(files) as file}
	<p>{file.name} ({file.size / 1000} Ko)</p>
	{/each}
{/if}
	
<style>
	
	h1 { 
		font-size: clamp(1rem, 10vw, 2rem); 
		margin-bottom: 20px;
	}

	p { 
		font-size: 1.4rem; 
	}

	input {
		position: absolute;
		width: 100%;
		height: 100%;
		opacity: 0;
	}

	input:hover {
		background: red;
	}

	label {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 75%;
		height: 100%;
		font-size: clamp(1.5rem, 5vw, 2.5rem);
		margin: 0 50px;
		cursor: pointer;
		text-align: center;
		line-height: normal;
	}

</style>