<!-- 关于 -->

<template>
    <div class="content about" id="about">
        <ModuleHeader :title="about.header.title" :sub-title="about.header.subtitle"/>

        <a-row type="flex" justify="center" align="top">

            <a-col class="col" :xs="24" :sm="24" :md="24" :lg="10" :xl="8">
                <img data-aos="fade-in" class="avatar" draggable="false" src="../assets/about/avatar_about.jpg"/>
            </a-col>

            <a-col class="color-content col" :xs="24" :sm="24" :md="24" :lg="14" :xl="16">

                <span data-aos="fade-in" class="title color-title">
                <vue-typer :text="about.header.subtitle" :type-delay='200' eraseStyle='select-all'></vue-typer>
                </span>
                
                <p class="lead">
                    Hello, I'm <strong>Mochammad Tedy Fazrin</strong> a Software Engineer based in Tangerang, Indonesia. Find me on
                    <template v-for="(social, idx) in about.social">
                    <a
                        :key="idx"
                        :href="social.link"
                        :style="{color: social.color}"
                        target="_blank">
                        {{ social.name }}
                    </a>
                    {{ idx !== about.social.length - 1 ? ', ': ''}}{{ idx === about.social.length - 2 ? 'and': ''}}
                    </template>
                </p>
                <p>
                    As a Software Engineer, I would like to bring technology to make life easier and increase productivity. I also want to create great products which have good design architecture, high scalability and easy to maintain.
                </p>
                <p>
                    I'm looking for opportunities to participate in challenging projects!
                </p>
            </a-col>
        </a-row>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import ModuleHeader from '@/components/module/ModuleHeader.vue';
    import ModuleSkeleton from '@/components/module/ModuleSkeleton.vue';
    import {Module} from '@/api/user_interface';
    // tslint:disable-next-line:no-var-requires
    import {VueTyper} from 'vue-typer';
    // tslint:disable-next-line:no-var-requires
    import VueMarkdown from 'vue-markdown';

    @Component({
        components: {
            ModuleHeader,
            ModuleSkeleton,
            VueTyper,
            VueMarkdown,
        },
        computed: {
            about(): Module {
                return this.$store.getters.getModule('about');
            },
        },
        methods: {
            /**
             * 检测是否为url
             * @param content 需要检测的内容
             */
            isUrl(content: string): boolean {
                const strRegex = '^(((https|http|ftp|rtsp|mms):)?//)'
                    + '?(([0-9a-z_!~*\'().&=+$%-]+: )?[0-9a-z_!~*\'().&=+$%-]+@)?' // ftp的user@
                    + '(([0-9]{1,3}.){3}[0-9]{1,3}' // IP形式的URL- 199.194.52.184
                    + '|' // 允许IP和DOMAIN（域名）
                    + '([0-9a-z_!~*\'()-]+.)*' // 域名- www.
                    + '([0-9a-z][0-9a-z-]{0,61})?[0-9a-z].' // 二级域名
                    + '[a-z]{2,6})' // first level domain- .com or .museum
                    + '(:[0-9]{1,4})?' // 端口- :80
                    + '((/?)|' // a slash isn't required if there is no file name
                    + '(/[0-9a-z_!~*\'().;?:@&=+$,%#-]+)+/?)$';
                const re = new RegExp(strRegex);
                return re.test(content);
            },
        },
        filters: {
            /**
             * 简化url
             * @param url
             */
            simplifyUrl(url: string): string {
                const strRegex = /^(((https|http|ftp|rtsp|mms):)?\/\/)?/;
                return url.replace(strRegex, '');
            },
        },
    })
    export default class About extends Vue {
    }
</script>

<style scoped lang="scss">
    @import '../styles/variable';

    .lead {
        margin-top: 1rem;
    }

    .about {
        .col {
            padding: 0 1rem;
        }

        .avatar {
            display: block;
            width: 100%;
            border-radius: 5px;
        }

        .title {
            letter-spacing: 5px;
            text-transform: uppercase;
            
        }

        .brief {
            display: block;
            margin: 1rem auto;
        }

        @media screen and (max-width: $--screen-md-min) {
            .col {
                padding: 0;
                &.color-content {
                    margin-top: 1.5rem;
                }
            }
        }

        .keys-row {
            margin: 1rem auto;

            .keys-col {
                margin: .5rem auto;
                word-break: break-all;
                padding-right: 1rem;

                .key {
                    margin-right: .5rem;
                    font-weight: bold;
                }

                .value {
                    color: inherit;
                    text-decoration: underline;
                }
            }
        }
    }
</style>
