<script>
    import {onMount} from 'svelte';

    let data;
    let error;

    let xValue;
    let yValue;

    const mapSize = 20; // Rozmiar mapy

    onMount(() => {
        // Main function to communicate with server
        const serverRequest = async (/** @type {any} */ serverAddress, /** @type {any} */ fetchArgument) => {
            try {
                const response = await fetch(`http://${serverAddress}/${fetchArgument}`, {
                    method: 'GET'
                });

                if (response.ok) {
                    return await response.json(); // Parse and set the data
                } else {
                    return null;
                }
            } catch (err) {
                error = 'Fetch failed: ' + (err instanceof Error ? err.message : 'Unknown error');
            }
        };

        // Function to get player position
        const getPlayerPosition = async () => {
            const data = await serverRequest('127.0.0.1:4000', 'get_position');
            if (data && 'x' in data && 'y' in data) {
                const positionX = parseInt(String(data.x), 16);
                const positionY = parseInt(String(data.y), 16);
                updatePlayerPosition(positionX, positionY);
            } else {
                console.error('x or y property is missing in the response data');
            }
        };

        const movePlayerForward = () => {
            console.log('move forward used');
            serverRequest('127.0.0.1:4000', 'move_forward');
        };
        const movePlayerLeft = () => {
            console.log('move left used');
            serverRequest('127.0.0.1:4000', 'move_left');
        };
        const movePlayerDown = () => {
            console.log('move down used');
            serverRequest('127.0.0.1:4000', 'move_down');
        };
        const movePlayerRight = () => {
            console.log('move right used');
            serverRequest('127.0.0.1:4000', 'move_right');
        };

        // Generate screen
        const screen = /** @type {HTMLCanvasElement} */ (document.querySelector('.screen'));
        const ctx = screen.getContext('2d');
        if (!ctx) {
            console.error('Failed to get 2D context from canvas.');
            return;
        }

        const updatePlayerPosition = (/** @type {number} */ x, /** @type {number} */ y) => {
            console.log('Plater position updated' + x + ' ' + y);
            ctx.clearRect(0, 0, screen.width, screen.height);
            ctx.fillRect(x * 10, y * 10, 10, 10);
        };

        setInterval(getPlayerPosition, 5000, '127.0.0.1:4000', 'get_position');
        // ctx.fillRect(10, 10, 10, 10);

        const buttons = document.querySelectorAll('.keyboard_btn');
        buttons[0].addEventListener('click', movePlayerForward);
        buttons[1].addEventListener('click', movePlayerLeft);
        buttons[2].addEventListener('click', movePlayerDown);
        buttons[3].addEventListener('click', movePlayerRight);
    });
</script>

<canvas class="screen" width="300" height="300"></canvas>
<div class="keyboard">
    <button class="keyboard_btn keyboard_btn-up">Up</button>
    <button class="keyboard_btn keyboard_btn-left">Left</button>
    <button class="keyboard_btn keyboard_btn-down">Down</button>
    <button class="keyboard_btn keyboard_btn-right">Right</button>
</div>

<style>
    .screen {
        display: grid;
        grid-template-columns: repeat(20, 1fr);
        grid-template-rows: repeat(20, 1fr);
        gap: 1px;
        border: 4px solid black;
        margin-bottom: 2rem;
    }

    :global(.cell) {
        width: 2rem;
        height: 2rem;

        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0.2rem;
    }

    :global(.active) {
        background-color: var(--main);
        border-radius: 50%;
    }

    .keyboard {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(2, 1fr);
    }

    .keyboard_btn {
        padding: 1rem;
        margin: 0.2rem;
        cursor: pointer;
        background-color: rgba(255, 255, 255, 0.4);
        transition: background-color 0.3s;
    }

    .keyboard_btn:hover {
        background-color: var(--main);
    }

    .keyboard_btn-up {
        grid-column: 2 / 3;
        grid-row: 1 / 2;
    }

    .keyboard_btn-left {
        grid-column: 1 / 2;
        grid-row: 2 / 3;
    }

    .keyboard_btn-down {
        grid-column: 2 / 3;
        grid-row: 2 / 3;
    }

    .keyboard_btn-right {
        grid-column: 3 / 4;
        grid-row: 2 / 3;
    }
</style>
