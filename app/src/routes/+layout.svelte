<script>
    import Header from './Header.svelte';
    import '../app.css';
</script>

<div class="app">
    <Header />

    <main>
        <slot />
    </main>

    <footer>
        <p>
            &copy<span class="footer_year"></span>
            <span class="footer_title">Stu The End</span> - Visoft Academy
        </p>
    </footer>
</div>

<style>
    @import '../lib/colors/colors.css';

    .app {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    main {
        flex: 1;
        display: flex;
        flex-direction: column;
        padding: 1rem;
        width: 100%;
        max-width: 64rem;
        margin: 0 auto;
        box-sizing: border-box;
    }

    footer {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 12px;
    }

    .footer_title {
        color: var(--main);
        font-weight: bold;
    }

    @media (min-width: 480px) {
        footer {
            padding: 12px 0;
        }
    }
</style>
