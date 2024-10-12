<script>
    import {onMount} from 'svelte';

    const mapSize = 20; // Rozmiar mapy
    let position = [mapSize / 2, mapSize / 2]; // Initial position

    onMount(() => {
        // Generate screen
        const screen = document.querySelector('.screen');

        for (let i = 0; i < mapSize * mapSize; i++) {
            const cell = document.createElement('div');
            cell.classList.add('cell');
            cell.textContent = i.toString();
            screen?.appendChild(cell);
        }

        let activeCell = screen?.querySelector(`.cell:nth-child(${1 + position[0] + position[1] * mapSize})`);
        activeCell?.classList.toggle('active');

        // Function to visualise player move on screen
        const setCellActive = (/** @type {number} */ x, /** @type {number} */ y) => {
            activeCell?.classList.toggle('active');
            activeCell = screen?.querySelector(`.cell:nth-child(${1 + x + y * mapSize})`);
            activeCell?.classList.toggle('active');
        };

        const useButtonUp = () => {
            if (position[1] > 0) {
                position[1]--;
            }
            console.log(position);
            setCellActive(position[0], position[1]);
        };
        const useButtonLeft = () => {
            if (position[0] > 0) {
                position[0]--;
            }
            console.log(position);
            setCellActive(position[0], position[1]);
        };
        const useButtonDown = () => {
            if (position[1] < mapSize - 1) {
                position[1]++;
            }
            console.log(position);
            setCellActive(position[0], position[1]);
        };
        const useButtonRight = () => {
            if (position[0] < mapSize - 1) {
                position[0]++;
            }
            console.log(position);
            setCellActive(position[0], position[1]);
        };

        const buttons = document.querySelectorAll('.keyboard_btn');
        buttons[0].addEventListener('click', useButtonUp);
        buttons[1].addEventListener('click', useButtonLeft);
        buttons[2].addEventListener('click', useButtonDown);
        buttons[3].addEventListener('click', useButtonRight);
    });
</script>

<div class="screen"></div>
<!-- Kontener dla mapy -->
<div class="keyboard">
    <button class="keyboard_btn keyboard_btn-up">Up</button>
    <button class="keyboard_btn keyboard_btn-left">Left</button>
    <button class="keyboard_btn keyboard_btn-down">Down</button>
    <button class="keyboard_btn keyboard_btn-right">Right</button>
    <!-- <p>Sterowanie</p> -->
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
