<script>
	import htmlToImage from 'html-to-image'
	import FileSaver  from 'file-saver'
	
	const image = 'https://images.weserv.nl/?url=https://telegra.ph/file/0020d15b9dd16834dfca9.jpg'
	
	let text = 'Orang Jahat Terlahir Dari Orang Baik Yang Tersakiti'
	let config = {
		align: 'center',
		position: 'top',
		size: 5
	}
	$: hasil = () => {
		return text.replace(/a|u|e|o/g, 'i').replace(/A|U|E|O/g, 'I')
	}
	
	const save = () => {
		htmlToImage.toBlob(document.getElementById('hasil'))
			.then(function (blob) {
				const fname = hasil().length > 36 ? hasil().slice(0,36) + '... - [alfianokt.github.io/nyinyir].jpg' : hasil() + ' - [alfianokt.github.io/nyinyir].jpg'
				saveAs(blob, fname)
			})
			.catch(function (error) {
				console.error('oops, something went wrong!', error);
			})
	}
</script>

<style>
@import 'https://unpkg.com/spectre.css@0.5.8/dist/spectre.min.css';
@import 'https://unpkg.com/spectre.css@0.5.8/dist/spectre-exp.min.css';
</style>

<div class="container">
  <div class="columns">
		<div class="column col-md-12 col-6 col-mx-auto mt-2">
			<div class="card">
				<div class="card-header">
					<div class="card-title h5">Tukang Nyinyir</div>
					<div class="card-subtitle text-gray">
						Nyinyir Generator by
						<a href="https://www.instagram.com/alfian_oktafireza?s=nyinyir" target="_blank">Alfian</a>
					</div>
				</div>
				<div class="card-body">
					<div class="form-group">
						 <label class="form-label" for="input-text">Masukkan Kata</label>
						<textarea class="form-input" placeholder="Masukkan teks disini" id="input-text" bind:value={text} />
					</div>
					<div class="form-group">
						<label class="form-label">Align Text (Perataan Teks)</label>
						<button 
							class="btn btn-sm form-inline"
							class:btn-primary={config.align == 'left'}
							on:click={() => config.align = 'left'}>
							Kiri
						</button>
						<button 
							class="btn btn-sm form-inline"
							class:btn-primary={config.align == 'center'}
							on:click={() => config.align = 'center'}>
							Tengah
						</button>
						<button 
							class="btn btn-sm form-inline"
							class:btn-primary={config.align == 'right'}
							on:click={() => config.align = 'right'}>
							Kanan
						</button>
						<button 
							class="btn btn-sm form-inline"
							class:btn-primary={config.align == 'justify'}
							on:click={() => config.align = 'justify'}>
							Kanan - Kiri
						</button>
					</div>
					<div class="form-group">
						<label class="form-label">Posisi Teks</label>
						<button 
							class="btn btn-sm form-inline"
							class:btn-primary={config.position == 'top'}
							on:click={() => config.position = 'top'}>
							Atas
						</button>
						<button 
							class="btn btn-sm form-inline"
							class:btn-primary={config.position == 'bottom'}
							on:click={() => config.position = 'bottom'}>
							Bawah
						</button>
					</div>
					<div class="form-group">
						<label class="form-label">Ukuran Teks</label>
						<input class="slider tooltip" oninput="this.setAttribute('value', this.value);" type="range" min="1" max="6" bind:value={config.size}>
					</div>
				</div>
			</div>
		</div>
    <div class="column col-md-12 col-6 col-mx-auto mt-2">
			<div class="card">
				<div class="card-body columns">
					<div class="card" id="hasil">
						{#if config.position == 'top'}
						<div
							class="card-title mx-1"
							class:h1={config.size == 6}
							class:h2={config.size == 5}
							class:h3={config.size == 4}
							class:h4={config.size == 3}
							class:h5={config.size == 2}
							class:h6={config.size == 1}
								 
							class:text-left={config.align == 'left'}
							class:text-center={config.align == 'center'}
							class:text-right={config.align == 'right'}
							class:text-justify={config.align == 'justify'}
						>
							{hasil()}
						</div>
						{/if}
						<div class="card-image">
							<img src={image} alt="Image Master" class="img-responsive">
						</div>
						{#if config.position == 'bottom'}
						<div
							class="card-title mx-1"
							class:h1={config.size == 6}
							class:h2={config.size == 5}
							class:h3={config.size == 4}
							class:h4={config.size == 3}
							class:h5={config.size == 2}
							class:h6={config.size == 1}
								 
							class:text-left={config.align == 'left'}
							class:text-center={config.align == 'center'}
							class:text-right={config.align == 'right'}
							class:text-justify={config.align == 'justify'}
						>
							{hasil()}
						</div>
						{/if}
					</div>
					<div class="mt-2">
						<button class="btn" on:click={save}>Simpan Ke Galeri</button>
					</div>
				</div>
			</div>
		</div>
  </div>
</div>