<template>
    <div class='d-flex justify-content-center align-items-center bg-secondary' style='min-height: 100vh'>
        <Timer v-if='!isSmallScreen'></Timer>
        <div v-else class='d-flex flex-fill flex-column gap-4 justify-content-between'>
            <div class='d-flex flex-fill bg-gradient-warning' style='height: 100px;'></div>
            <div class='container d-flex flex-column align-items-center text-center p-3 gap-3'>
                <span class='fs-1 fw-bold text-uppercase' style='color: #FFFF'> Sorry, but this page doesn't support mobile devices </span>
                <span class='fs-6 fw-bold text-uppercase' style='color: #FFFF'> If you're using a tablet and seeing this, please try rotating it horizontally </span>
            </div>
            <div class='d-flex flex-fill bg-gradient-warning' style='height: 100px;'></div>
        </div>
    </div>
</template>

<script lang='ts' scoped>
import { Vue, Options } from 'vue-class-component';
import './core/styles.scss';
import { Timer } from './components';

@Options({
    name: 'App',
    components: {
        Timer
    }
})
export default class App extends Vue {
    public isSmallScreen = true;

    public created(): void {
        window.addEventListener('resize', this.handleResize);
        screen.orientation.addEventListener('change', this.handleResize);
    }

    public mounted(): void {
        this.handleResize();
    }

    public handleResize(): void {
        this.isSmallScreen = true;
        new Promise(() => setTimeout(() => {
            this.isSmallScreen = window.innerWidth < 1000 || window.innerHeight < 635;
        }, 100));
    }
}
</script>
