<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
    <div class="hello">
        <!-- wwManager:start -->
        <wwSectionEditMenu v-bind:sectionCtrl="sectionCtrl"></wwSectionEditMenu>
        <!-- wwManager:end -->

        <!-- Weweb Wallpaper -->
        <wwObject class="background" v-bind:ww-object="section.data.wewebWP" ww-category="background">
        </wwObject>

        <div class="content">
            <!-- Hello world ! -->
            <wwObject v-bind:ww-object="section.data.helloWorld">
            </wwObject>
        </div>

    </div>
</template>

<!-- This is your Javascript -->
<!-- ✨ Here comes the magic ✨ -->
<script>
export default {
    name: "hello-world",
    props: {
        // The section controller object is passed to you.
        sectionCtrl: Object
    },
    data() {
        return {
        }
    },
    computed: {
        //Get the section object here !
        // It contains all the info and data about the section
        // Use it has you like !
        section() {
            return this.sectionCtrl.get();
        }
    },
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

    },
    methods: {
    }
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
</style>
