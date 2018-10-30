<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
    <div class="hello">

        <!-- Weweb Wallpaper -->
        <wwObject class="background" v-bind:ww-object="section.data.wewebWP" v-bind:section="section" ww-category="background"></wwObject>

        <!--
            <div class="movingBg" v-bind:class="{'fixed': progress > 0}">
                <wwObject class="background" v-bind:ww-object="section.data.wewebWP" v-bind:section="section" ww-category="background"></wwObject>
                <div class="overlay" v-bind:style="opacity"></div>
                <div class="border vert left" v-bind:style="vertScale"></div>
                <div class="border vert right" v-bind:style="vertScale"></div>
                <div class="border hor top" v-bind:style="horScale"></div>
                <div class="border hor bottom" v-bind:style="horScale"></div>
            </div>
        -->

        <div class="content">
            <!-- Hello world ! -->
            <wwObject v-bind:ww-object="section.data.helloWorld" v-bind:section="section"></wwObject>
        </div>

    </div>
</template>

<!-- This is your Javascript -->
<!-- ✨ Here comes the magic ✨ -->
<script>
export default {
    name: "hello-world",
    props: {
        // The section object is passed to you.
        // It contains all the info and data about the section
        // Use it has you like !
        section: Object
    },
    /*/
        data() {
            return {
                progress: 0
            }
        },
        
        computed: {
            vertScale() {
                return {
                    transform: 'scale(' + (1 - this.progress) + ', 1)'
                }
            },
            horScale() {
                return {
                    transform: 'scale(1,' + (1 - this.progress) + ')'
                }
            },
            opacity() {
                return {
                    opacity: this.progress
                }
            }

        },
    /**/
    created() {

        //Initialize section data
        this.section.data = this.section.data || {};

        //Initialize helloWorld text
        if (!this.section.data.helloWorld) {
            this.section.data.helloWorld = wwLib.wwObject.getDefault({
                type: 'ww-text',
                data: {
                    text: {
                        fr_FR: 'Hello World !',
                        en_GB: 'Hello World !'
                    },
                    align: 'center',
                    size: 4,
                    color: 'white'
                }
            });
        }

        //Initialize image
        if (!this.section.data.wewebWP) {
            this.section.data.wewebWP = wwLib.wwObject.getDefault({
                type: 'ww-image',
                data: {
                    url: 'http://cdn.wewebapp.io/public/images/weweb-wp.png'
                }
            });
        }

        /*/
            window.addEventListener('scroll', this.onScroll);
        /**/
    },
    /*/
        methods: {
            onScroll(event) {
                const sectionTop = this.$el.getBoundingClientRect().y,
                    clientHeight = document.documentElement.clientHeight;

                if (sectionTop > 0) {
                    this.progress = 0;
                }
                else if (sectionTop <= 0 && clientHeight * 2 - sectionTop > 0) {
                    this.progress = Math.max(Math.min(-sectionTop / clientHeight * 2, 1), 0);
                }
                else {
                    this.progress = 1;
                }
            }
        },
        beforeDestroy() {
            window.removeEventListener('scroll', this.onScroll);
        }
    /**/
};
</script>

<!-- This is your CSS -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add lang="scss" or others to use computed CSS -->
<style scoped>
.hello {
  padding: 100px 50px;
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
}

.content {
  position: relative;
}

/*/
    .hello {
        flex-basis: 200%;
    }

    .content {
    position: absolute;
    top: 50%;
    left: 150px;
    }

    .movingBg {
    position: absolute;
    top: 0;
    left: 0;
    height: 50%;
    width: 100%;
    }

    .movingBg.fixed {
    top: 0;
    bottom: 0;
    height: auto;
    position: fixed;
    }

    .border {
    background-color: white;
    position: absolute;
    z-index: 2;
    }

    .border.hor {
    left: 0;
    width: 100%;
    height: 75px;
    }

    .border.vert {
    top: 0;
    height: 100%;
    width: 75px;
    }

    .border.top {
    top: 0;
    transform-origin: 50% 0;
    }

    .border.bottom {
    bottom: 0;
    transform-origin: 50% 100%;
    }

    .border.left {
    left: 0;
    transform-origin: 0 50%;
    }

    .border.right {
    right: 0;
    transform-origin: 100% 50%;
    }

    .overlay {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.2);
    z-index: 1;
    }
/**/
</style>
