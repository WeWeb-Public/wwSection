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
        <wwObject class="background" v-bind:ww-object="section.data.color" ww-category="background"></wwObject>

        <div class="content">
            <!-- Hello world ! -->
            <wwObject v-bind:ww-object="section.data.helloWorld"></wwObject>
            <wwObject class="hello-image" v-bind:ww-object="section.data.image1"></wwObject>

            <!-- LIST -->
            <wwLayoutColumn tag="div" ww-default="ww-text" :ww-list="section.data.list" class="list" @ww-add="add(section.data.list, $event)" @ww-remove="remove(section.data.list, $event)">
                <wwObject tag="div" v-for="object in section.data.list" :key="object.uniqueId" :ww-object="object"></wwObject>
            </wwLayoutColumn>
        </div>
    </div>
</template>

<!-- This is your Javascript -->
<!-- ✨ Here comes the magic ✨ -->
<script>
export default {
    name: "__COMPONENT_NAME__",
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
        let needUpdate = false

        this.section.data = this.section.data || {};

        //Initialize content
        if (!this.section.data.helloWorld) {
            this.section.data.helloWorld = wwLib.wwObject.getDefault({
                type: 'ww-text',
                data: {
                    text: {
                        fr_FR: 'Hello World FR !',
                        en_GB: 'Hello World !'
                    }
                }
            });
            needUpdate = true
        }

        if (!this.section.data.color) {
            this.section.data.color = wwLib.wwObject.getDefault({
                type: 'ww-color'
            });
            needUpdate = true
        }

        if (!this.section.data.image1) {
            this.section.data.image1 = wwLib.wwObject.getDefault({
                type: 'ww-image'
            });
            needUpdate = true
        }

        if (!this.section.data.list) {
            this.section.data.list = [];
            needUpdate = true;
        }


        if (needUpdate) {
            this.sectionCtrl.update(this.section);
        }

    },
    methods: {
        /* wwManager:start */
        add(list, options) {
            try {
                list.splice(options.index, 0, options.wwObject);
                this.sectionCtrl.update(this.section);
            } catch (error) {
                wwLib.wwLog.error('ERROR : ', error);
            }
        },
        remove(list, options) {
            try {
                list.splice(options.index, 1);
                this.sectionCtrl.update(this.section);
            } catch (error) {
                wwLib.wwLog.error('ERROR : ', error);
            }
        },
        /* wwManager:end */

    }
};
</script>

<!-- This is your CSS -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add lang="scss" or others to use computed CSS -->
<style lang="scss" scoped>
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
    .hello-image {
        width: 200px;
    }
    .list {
        margin-top: 20px;
        width: 50%;
        margin-left: 25%;
    }
}
</style>
