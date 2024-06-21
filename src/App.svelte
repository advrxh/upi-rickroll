<script>
	import Qr from "./components/QR.svelte";

	var contextRaw = "upi@gpay";
	var context = "upi@gpay";
	var app = "gpay";
	let QrComponent;

	const handleButtonClick = () => {
		QrComponent.saveAsImage();
	}

	const isEven = () => {
		var num = Math.floor(Math.random() * 69 * 420);
		return num % 2 == 0;
	};

	const rolls = {
		gpay: "https://boulderbugle.com/google-pay-LeaxPh8J",
		paytm: "https://boulderbugle.com/paytm-m3gYXJLI",
		phonepe: "https://boulderbugle.com/phonepe-GipYBC7c",
	};

	const setQrContext = () => {
		var rando = isEven();
		if (rando) {
			context = contextRaw;
		} else {
			context = rolls[app];
		}
	};

</script>

<main>
	<div id="head">
		<h1>Theres a 50-50 chance it's a rickroll</h1>
	</div>

	<div id="context">
		<button id="roll">
			<img src="astley.gif" alt="astley" width="64px" height="64px" />
		</button>
		<input
			type="text"
			name="contextData"
			id="context-data"
			placeholder="Enter UPI ID, Theres a 50-50 chance it's a rickroll"
			bind:value={contextRaw}
		/>
		<button id="update" on:click={() => setQrContext()}>Create a QR</button>
	</div>

	<div id="apps">
		<ul>
			<li id="paytm">
				<button
					on:click={() => {
						app = "paytm";
						context = contextRaw = "upi@paytm"
					}}
					><img src="paytm.png" alt="paytm" width="80px" />
				</button>
			</li>
			<li id="gpay">
				<button
					on:click={() => {
						app = "gpay";
						context = contextRaw = "upi@gpay"
					}}
					><img src="gpay.png" alt="gpay" width="128px" />
				</button>
			</li>

			<li id="phonepe">
				<button
					on:click={() => {
						app = "phonepe";
						context = contextRaw = "upi@phonepe"
					}}
					><img src="phonepe.png" alt="phonepe" width="128px" />
				</button>
			</li>
		</ul>
	</div>

	<div id="qr">
			<Qr bind:this={QrComponent} url={context} app={app}  />
	</div>



	<p>Double click merchant name and phone to update it.</p>
    <button id="saveBtn" on:click={handleButtonClick}>Save as Image</button>
</main>

<style>
	:root {
		--bong: rgb(235, 77, 20);
	}

	main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	main button:hover {
		cursor: pointer;
	}

	#context {
		padding: 1em;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	#roll {
		background: transparent;
		border: none;
		margin: 2em;
		transition: all 0.2s;
	}

	#roll:hover {
		transform: scale(120%);
	}

	#context-data {
		width: 60%;
		margin: 1em;
		padding: 1em;
		border: none;
		box-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
		border-color: #333333;
		background-color: #333333;
		border-radius: 6px;
		color: white;
	}

	#context-data::placeholder {
		color: var(--bong);
	}

	#update {
		margin: 2em;
		border: 4px solid var(--bong);
		background-color: #333333;
		color: var(--bong);
		padding: 0.7em;
		border-radius: 10px;
		transition: all 0.2s;
	}

	#update:hover {
		transform: scale(105%);
		font-weight: bold;
	}

	#apps {
		width: 100%;
		padding: 1em;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: row;
	}
	
	ul {
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		list-style: none;
	}

	li {
		margin: 1em;
	}

	li button {
		background: whitesmoke;
		border: 2px solid var(--bong);
		width: 200px;
		height: 60px;
		border-radius: 10px;
		transition: all 0.2s;
	}

	li button:hover {
		box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.5);
	}

	#head {
		width: 100%;
		display:  flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		color: var(--bong);
	}

	#qr {

        width: 360px;
        height: 550px;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        border-radius: 20px;
        box-shadow:
            rgba(0, 0, 0, 0.25) 0px 54px 55px,
            rgba(0, 0, 0, 0.12) 0px -12px 30px,
            rgba(0, 0, 0, 0.12) 0px 4px 6px,
            rgba(0, 0, 0, 0.17) 0px 12px 13px,
            rgba(0, 0, 0, 0.09) 0px -3px 5px;
	}

    #saveBtn {
		margin-bottom: 2em;
		font-weight: bold;
        border: 1px solid #bbb;
        color: var(--bong);
    }
	p {
		margin-top: 2em;
		color: #333333;
		font-weight: bold;
	}
</style>
