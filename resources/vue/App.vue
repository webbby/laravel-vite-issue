<template>
    <p>Hello</p>
    <component is="DynamicThemeComponent"/>
</template>

<script>
const file = './Foo.vue';
import {defineAsyncComponent} from "vue";
export default {
    name: "App",
    components: {
        DynamicThemeComponent: defineAsyncComponent(() => {
            return import(/* @vite-ignore */ file)
        })
    },
    methods: {
        reloadDynamicThemeComponent(componentPath) {
            this.$.components.DynamicThemeComponent = defineAsyncComponent(() => {
                return import(/* @vite-ignore */ componentPath)
            });
            this.$forceUpdate();
        }
    },
    mounted() {
        const self = this;
        setTimeout(() => {
            self.reloadDynamicThemeComponent('./Moo.vue')
        }, 2700)
    }
}
</script>

<style scoped>

</style>
