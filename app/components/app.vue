<template>
    <Page style="background-color:brown">
        <ActionBar title="Extra curicular" />
        <TabView>
            <TabViewItem title="Courses" class="h2 text-capitalize">
                <StackLayout>
                    <courseList :courses="courses" @addCourse="addToCart" />
                </StackLayout>
            </TabViewItem>
            <TabViewItem title="Checkout" class="h2 text-capitalize">
                <StackLayout>
                    <checkout :cart="cart" :courses="courses"
                        @removeCourse="removeFromCart" />
                </StackLayout>
            </TabViewItem>
        </TabView>
    </Page>
</template>

<script>
    import courseList from "./courseList";
    import checkout from "./checkout";
    export default {
        data() {
            return {
                cart: [],
                courses: []
            };
        },
        created: function() {
            fetch("https://individual2cw.herokuapp.com/collection/lesson")
                .then(r => r.json())
                .then(response => {
                    this.courses = response;
                })
                .catch(e => {});
        },
        components: {
            courseList,
            checkout
        },
        methods: {
            addToCart(course) {
                this.cart.push(course);
            },
            removeFromCart(course) {
                const index = this.cart.indexOf(course);
                if (index > -1) {
                    this.cart.splice(index, 1);
                }
                course.spaces++;
            }
        }
    };
</script>

<style>
</style>
