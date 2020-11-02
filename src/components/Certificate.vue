<template>
    <div class="content" id="certificate">
        <ModuleHeader :title="certificate.header.title" :sub-title="certificate.header.subtitle"/>
        <a-timeline>
            <a-timeline-item data-aos="fade-in" v-for="card in certificate.cards" v-bind:key="card.title + card.subtitle">
                <a-card class="certificate-card" :bordered="true" style="width: 100%">
                <div class="wrapper ">
                    <div class="cert-badge ">
                        <a :href="card.link" target="_blank">
                            <a-avatar :shape="'square'" :size="80" :src="card.icon" alt="" />
                        </a>
                        </div>
                        <div class="cert-content">
                        <h4 style="margin-bottom: .25rem!important;"><a :href="card.link" target="_blank">{{ card.title }}</a></h4>
                        <div>{{ card.subtitle }}</div>
                        <div style="margin-top: 1rem!important;">{{ card.md }}</div>
                        </div>
                    </div>
                <!-- <a-card class="certificate-card" :bordered="true" style="width: 100%">
                    <template slot="title">
                        <h1 class="title">{{card.title}}</h1>
                        <span v-if="!!card.subtitle" class="sub-title">{{card.subtitle}}</span>
                    </template>
                    <vue-markdown>{{card.md}}</vue-markdown> -->
                </a-card>
            </a-timeline-item>
        </a-timeline>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import ModuleHeader from '@/components/module/ModuleHeader.vue';
    import {Module} from '@/api/user_interface';
    // tslint:disable-next-line:no-var-requires
    import VueMarkdown from 'vue-markdown';

    @Component({
        components: {
            ModuleHeader,
            VueMarkdown,
        },
        computed: {
            certificate(): Module {
                return this.$store.getters.getModule('certificate');
            },
        },
    })
    export default class About extends Vue {
    }
</script>

<style scoped lang="scss">
    @import '../styles/variable';
    .certificate-card {
        .title {
            width: 100%;
            font-size: 1rem;
            overflow: scroll;
            margin: 0;
        }

        .sub-title {
            width: 100%;
            font-size: .7rem;
            display: block;
            margin-top: .5rem;
        }
    }
    .wrapper {
        display: flex;
        line-height: 1.5;
    }
    .cert-badge {
        width: 90px;
        height: 90px;
    }

    .cert-content {
        flex: 1;
    h4 {
        font-weight: 600;
    }
    }
</style>
