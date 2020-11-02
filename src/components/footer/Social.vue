<template>
    <div class="social" :style="{'font-size': size + 'em'}">
        <!-- github -->
        <a :style="{color: color}" :href="social['github'] || 'https://github.com/tedy69'" target="_blank"><a-icon type="github" /></a>
        <!-- twitter -->
        <a :style="{color: color}" :href="social['twitter'] || 'https://twitter.com/dark_dev69'" target="_blank"><a-icon type="twitter" /></a>
        <!-- linkedin -->
        <a :style="{color: color}" :href="social['linkedin'] || 'https://www.linkedin.com/in/mochammad-tedy-fazrin/'" target="_blank"><a-icon type="linkedin" /></a>
        <!-- instagram -->
        <a :style="{color: color}" :href="social['instagram'] || 'https://instagram.com/tedyfazrin_/'" target="_blank"><a-icon type="instagram" /></a>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import {mapGetters} from 'vuex';

    @Component({
        components: {
        },
        props: {
            color: String,
            size: Number,
        },
        computed: {
            ...mapGetters(['social']),
        },
    })
    export default class Social extends Vue {
    }
</script>

<style scoped lang="scss">
    .social {
        &>* {
            margin: 0.5em;
        }
    }
</style>

