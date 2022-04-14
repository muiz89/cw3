<template>
    <ListView for="course in courses" @itemTap="onItemTap" style="color:black;height:100%">
        <v-template>
            <GridLayout columns="70, auto, *" rows="90, auto, *" width="400"
                height="200" backgroundColor="blanchedalmond">
                <Label :text="`$${course.price}`" row="2" col="1" />
                <Label :text="course.location" row="2" col="2" rowSpan="2" />
                <Label :text="course.subject" row="1" col="1" />
            </GridLayout>
        </v-template>
    </ListView>
</template>

<script>
    export default {
        props: ["courses"],
        data() {
            return {};
        },
        methods: {
            onItemTap(event) {
                this.$emit("addCourse", event.item);
            }
        }
    };
</script>
