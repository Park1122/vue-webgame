<template>
    <div v-if="currentGame === 'number-baseball'">
        <number-baseball></number-baseball>
    </div>
    <div v-else-if="currentGame === 'response-check'">
        <response-check></response-check>
    </div>
    <div v-else-if="currentGame === 'rock-scissors-paper'">
        <rock-scissors-paper></rock-scissors-paper>
    </div>
    <div v-else>일치하는 게임이 없습니다</div>
</template>

<script>
    import NumberBaseball from '../3.숫자야구/NumberBaseball';
    import ResponseCheck from '../4.반응속도체크/ResponseCheck';
    import RockScissorsPaper from '../5.가위바위보/RockScissorsPaper';

    export default {
        components: {
            NumberBaseball,
            ResponseCheck,
            RockScissorsPaper
        },
        mounted() {
            console.log(this.$route);
        },
        computed: {
            currentGame() {
                return this.$route.params.name;
            }
        }
    }
</script>