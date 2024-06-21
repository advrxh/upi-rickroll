<script>
    import html2canvas from "html2canvas";
    export var url;
    export var app;

    var qrElement;

    let _phone = Math.floor(Math.random() * 10000000000);

    var vendor = {
        name: `${app.slice(0, 1).toUpperCase() + app.slice(1)} Payment Merchant`,
        phone: `+91 ${_phone}`,
    };

    $: {
        vendor.name = `${app.slice(0, 1).toUpperCase() + app.slice(1)} Payment Merchant`;
    }

    var clicked = {
        name: false,
        phone: false,
    };

    export const saveAsImage = async () => {
        try {
            const canvas = await html2canvas(qrElement, {
                useCORS: true,
                scale: window.devicePixelRatio,
                allowTaint: true,
                backgroundColor: null,
                logging: false,
            });
            const imgData = canvas.toDataURL("image/png");
            const link = document.createElement("a");
            link.href = imgData;
            link.download = "qr.png";
            link.click();
        } catch (error) {
            console.error("Error capturing image:", error);
        }
    };
</script>

<main>
    <div id="qr-content" bind:this={qrElement}>
        <div id="head">
            <img src={`${app}.png`} alt={app} width="200px" />
        </div>
        <div class="divider"></div>
        <div id="main-text">
            {#if clicked.name}
                <input
                    type="text"
                    name="nameInput"
                    bind:value={vendor.name}
                    on:mouseleave={() => {
                        clicked.name = !clicked.name;
                    }}
                    on:keypress={(e) => {
                        if (e.key == "Enter") {
                            clicked.name = !clicked.name;
                        }
                    }}
                />
            {:else}
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <h3
                    on:dblclick={() => {
                        clicked.name = !clicked.name;
                    }}
                >
                    {vendor.name}
                </h3>
            {/if}

            {#if clicked.phone}
                <input
                    type="text"
                    name="phoneInput"
                    bind:value={vendor.phone}
                    on:mouseleave={() => {
                        clicked.phone = !clicked.phone;
                    }}
                    on:keypress={(e) => {
                        if (e.key == "Enter") {
                            clicked.phone = !clicked.phone;
                        }
                    }}
                />
            {:else}
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <p
                    on:dblclick={() => {
                        clicked.phone = !clicked.phone;
                    }}
                >
                    {vendor.phone}
                </p>
            {/if}
        </div>
        <div id="qr">
            <img
                src={`https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=${url}`}
                alt="qr"
            />
        </div>
        <div id="bhim">
            <img src="bhim-upi.png" width="200px" alt="bhim" />
        </div>
    </div>
</main>

<style>
    main {
        width: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin: 3em;
    }
    #qr-content {
        width: 360px;
        height: 550px;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        flex-direction: column;
        border-radius: 20px;
        background-color: white;
    }
    #head {
        margin: 0.8em;
    }

    #main-text {
        text-align: center;
    }

    #main-text h3,
    #main-text p {
        color: #424242;
    }

    div .divider {
        width: 60%;
        height: 3px;
        background-color: #bbb;
    }
</style>
