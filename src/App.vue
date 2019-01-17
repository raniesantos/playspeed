<template>
    <div>
        <p>Duration (HH MM SS)</p>

        <input type="number" min="0" max="99" v-model.number="hh">
        <input type="number" min="0" max="59" v-model.number="mm">
        <input type="number" min="0" max="59" v-model.number="ss">

        <p>Duration in seconds {{ seconds }}</p>

        <hr>

        <p>Playback speed</p>
        <input type="number" min="1" max="2" step=".05" v-model.number="speed">

        <hr>

        <p>Watch Time {{ watchTime }} ({{ watchTimeInSeconds }} seconds)</p>
    </div>
</template>

<script>
export default {
    data () {
        return {
            hh: 0,
            mm: 0,
            ss: 0,
            speed: 1
        };
    },
    computed: {
        seconds () {
            return this.hh * 3600 + this.mm * 60 + this.ss;
        },
        watchTimeInSeconds () {
            return Math.ceil(this.seconds / this.speed);
        },
        watchTime () {
            const measuredTime = new Date(null);
            measuredTime.setSeconds(this.watchTimeInSeconds);
            return measuredTime.toISOString().substr(11, 8);
        }
    }
};
</script>

<style src="./style.css"></style>
