<template>
    <div class='d-flex bg-gradient-timer' style='width: 100vw; height: 75vh;'>
        <div class='d-flex' style='flex-grow: 0.5;'>
            <div class='d-flex bg-secondary' style='width: 10px; margin-left: 10px'></div>
        </div>
        <div class='d-flex flex-column' style='flex-grow: 0.5;'>
            <div class='d-flex' style='flex-grow: 0.9;'></div>
            <div class='d-flex flex-row-reverse bg-secondary border border-primary' style='flex-grow: 0.1; margin-right: 10px;'>
                <div class='d-flex flex-column gap-2 justify-content-evenly p-2' style='width: 25%;'>
                    <div class='d-flex justify-content-center border border-primary gap-4 px-2 py-1'>
                        <div class='d-flex flex-column'>
                            <span class='fs-1 text-primary'> 内部 </span>
                            <span class='fs-2 text-primary fw-bold'> INTERNAL </span>
                        </div>
                        <div class='d-flex flex-fill bg-gradient-warning'></div>
                    </div>
                    <div class='d-flex flex-column justify-content-center align-items-center border border-primary px-2 py-1'>
                        <span class='fs-3 text-primary'> 主電源供給システム </span>
                        <span class='fs-5 text-primary fw-bold'> MAIN ENERGY SUPPLY SYSTEM </span>
                    </div>
                    <div class='d-flex flex-column justify-content-center  border border-primary px-2 py-1'>
                        <span class='fs-1 text-primary'> 外部 </span>
                        <span class='fs-2 text-primary fw-bold'> EXTERNAL </span>
                    </div>
                </div>
                <div class='d-flex flex-column flex-fill justify-content-between px-2'>
                    <div class='d-flex gap-2 align-items-baseline'>
                        <span class='fs-1 text-primary'> 新年の残り時間 </span>
                        <span class='fs-2 text-primary'> NEW YEAR TIME REMAINING: </span>
                    </div>
                    <div class='d-flex align-items-baseline' style='width: 500px; height: 125px;'>
                        <span class='text-primary font-digital-number' style='font-size: 275px; line-height: 170px;'>{{ time.toFormat('HH:mm') }}</span>
                        <span class='text-primary font-digital-number' style='font-size: 200px; line-height: 170px;'>{{ time.toFormat(':ss') }}</span>
                    </div>
                    <div class='d-flex gap-5 justify-content-center'>
                        <div class='d-flex gap-3 align-items-baseline'>
                            <span class='fs-1 text-primary font-digital-number fw-bold'>{{ time.month }}</span>
                            <span class='fs-2 text-primary'>{{ ' MONTHS' }}</span>
                        </div>
                        <div class='d-flex gap-3 align-items-baseline'>
                            <span class='fs-1 text-primary font-digital-number fw-bold'>{{ time.daysInYear }}</span>
                            <span class='fs-2 text-primary'>{{ ' DAYS' }}</span>
                        </div>
                    </div>
                </div>
            </div>
            <div class='d-flex flex-row-reverse' style='flex-grow: 0.2; margin-right: 10px;;'>
                <div class='d-flex bg-secondary' style='width: 25%; height: 100%;'></div>
                <div class='d-flex flex-fill justify-content-evenly align-items-center'>
                    <div class='d-flex flex-column justify-content-center align-items-center bg-secondary border border-primary px-2 py-1' style='width: 7em'>
                        <span class='fs-4 text-primary'> STOP </span>
                        <div class='bg-success' style='width: 100%; height: 1.5em;'></div>
                    </div>
                    <div class='d-flex flex-column justify-content-center align-items-center bg-secondary border border-primary px-2 py-1' style='width: 7em'>
                        <span class='fs-4 text-primary'> SLOW </span>
                        <div class='bg-warning' style='width: 100%; height: 1.5em;'></div>
                    </div>
                    <div class='d-flex flex-column justify-content-center align-items-center bg-secondary border border-primary px-2 py-1' style='width: 7em'>
                        <span class='fs-4 text-primary'> NORMAL </span>
                        <div class='bg-primary' style='width: 100%; height: 1.5em;'></div>
                    </div>
                    <div class='d-flex flex-column justify-content-center align-items-center bg-secondary border border-primary px-2 py-1' style='width: 7em'>
                        <span class='fs-4 text-primary'> RACING </span>
                        <div class='bg-danger' style='width: 100%; height: 1.5em;'></div>
                    </div>
                </div>
            </div>
            <div class='d-flex bg-secondary' style='height: 10px; margin-right: 10px;'></div>
            <div class='d-flex' style='height: 1.5%;'></div>
            <div class='d-flex bg-secondary' style='flex-grow: 0.7;'></div>
        </div>
    </div>
</template>

<script lang='ts' scoped>
import { Vue, Options } from 'vue-class-component';
import { DateTime } from 'luxon';

@Options({
    components: {
    }
})
export default class Timer extends Vue {
    public time: DateTime = DateTime.now();

    public mounted(): void {
        setInterval(this.updateTimer, 1);
    }

    private updateTimer(): void {
        const now = DateTime.now();
        this.time = DateTime.fromObject({
            day: 1,
            month: 1,
            year: now.year + 1,
            hour: 0,
            minute: 0,
            millisecond: 0
        }).minus(now.toObject());
    }
}
</script>

<style scoped lang='scss'>
    .bg-gradient-timer {
        background: rgb(149,55,17);
        background: -moz-linear-gradient(90deg, rgba(149,55,17,1) 0%, rgba(166,149,35,1) 25%, rgba(70,112,30,1) 75%, rgba(69,76,128,1) 100%);
        background: -webkit-linear-gradient(90deg, rgba(149,55,17,1) 0%, rgba(166,149,35,1) 25%, rgba(70,112,30,1) 75%, rgba(69,76,128,1) 100%);
        background: linear-gradient(90deg, rgba(149,55,17,1) 0%, rgba(166,149,35,1) 25%, rgba(70,112,30,1) 75%, rgba(69,76,128,1) 100%);
        filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#953711',endColorstr='#454c80',GradientType=1);
    }
</style>