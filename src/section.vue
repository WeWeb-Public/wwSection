<!-- This is a Vue.js single file component. -->
<!-- Check the Vue.js doc here :  -->
<!-- https://vuejs.org/v2/guide/ -->

<!-- This is your HTML -->
<template>
    <div class="section-hello-world">
        <!-- wwManager:start -->
        <wwSectionEditMenu v-bind:sectionCtrl="sectionCtrl"></wwSectionEditMenu>
        <!-- wwManager:end -->

        <!-- This is the background of the section -->
        <wwObject class="background" v-bind:ww-object="section.data.background" ww-category="background"></wwObject>

        <div class="content-container">
            <!-- This is a simple WeWeb object which can be anything in the editor -->
            <wwObject class="title" v-bind:ww-object="section.data.title"></wwObject>

            <div class="content">
                <!-- This is another WeWeb object that we initiaze as an image -->
                <div class="left-container">
                    <wwObject class="image" v-bind:ww-object="section.data.image"></wwObject>
                </div>

                <!-- This is a content block, a list of objects, it will add the little blue "plus" around the objects in the editor -->
                <div class="right-container">
                    <wwLayoutColumn tag="div" ww-default="ww-text" :ww-list="section.data.contentList" class="list" @ww-add="add(section.data.contentList, $event)" @ww-remove="remove(section.data.contentList, $event)">
                        <wwObject tag="div" v-for="object in section.data.contentList" :key="object.uniqueId" :ww-object="object"></wwObject>
                    </wwLayoutColumn>
                </div>
            </div>
        </div>
    </div>
</template>

<!-- This is your Javascript -->
<!-- ✨ Here comes the magic ✨ -->
<script>
export default {
    name: '__COMPONENT_NAME__',
    props: {
        // The section controller object is passed. You can access it anytime
        sectionCtrl: Object
    },
    data() {
        return {};
    },
    computed: {
        // The section object contains all the info and data about the section
        // Use it as you like !
        section() {
            return this.sectionCtrl.get();
        }
    },
    created() {
        // Initialize the data once the section is created in the DOM
        this.init();
    },
    methods: {
        init() {
            // Initialize section data
            let needUpdate = false;

            // We will only save the data in this.section.data
            // So you need to put in there all the data of you WeWeb objects
            this.section.data = this.section.data || {};

            // Initialize WeWeb objects that are in the html template up there
            if (!this.section.data.background) {
                this.section.data.background = wwLib.wwObject.getDefault({ type: 'ww-color' });
                needUpdate = true;
            }

            if (!this.section.data.title) {
                this.section.data.title = wwLib.wwObject.getDefault({
                    type: 'ww-text',
                    data: {
                        text: {
                            fr: 'Hello World FR !',
                            en: 'Hello World !'
                        }
                    }
                });
                needUpdate = true;
            }

            if (!this.section.data.image) {
                this.section.data.image = wwLib.wwObject.getDefault({ type: 'ww-image' });
                needUpdate = true;
            }

            if (!this.section.data.contentList) {
                this.section.data.contentList = [];
                needUpdate = true;
            }

            if (needUpdate) {
                this.sectionCtrl.update(this.section);
            }
        },
        // --------- EDITOR FUNCTIONS ---------
        // All the codes between /* wwManager:start */ and /* wwManager:end */ are only for editor purposes
        // So It won't in the published website!
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
        }
        /* wwManager:end */
    }
};
</script>

<!-- This is your CSS -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add lang="scss" or others to use computed CSS -->
<style lang="scss" scoped>
.section-hello-world {
    .background {
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
    }
    .content-container {
        position: relative;
        max-width: 1200px;
        padding: 25px;
        margin: auto;
        .title {
            margin: 20px 0;
        }
        .content {
            position: relative;
            display: flex;
            justify-content: space-between;
            align-items: center;
            .left-container,
            .right-container {
                width: 45%;
            }
        }
    }
}
</style>
