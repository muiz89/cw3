<template>
    <StackLayout>
        <Label class="h1 text-center" text="Cart" style="color:white" />
        <Label class="h5 text-center" text="tap to remove"
            style="color:white" />
        <ListView for="course in cart" @itemTap="onItemTap"
            style="color:white; height:50%">
            <v-template>
                <StackLayout>
                    <Label :text="`Subject: ${course.subject}`" />
                    <Label :text="`price: ${course.price}`" />
                    <Label
                        :text="`available Inventory: ${course.availableInventory}`" />
                </StackLayout>
            </v-template>
        </ListView>
        <TextField style="color:white;" hint=" name"
            v-model="checkout.name" />
        <TextField style="color:white;" hint=" phone number"
            v-model="checkout.phone" />
        <Button @tap="submit" text="checkout" />
    </StackLayout>
</template>

<script>
    export default {
        props: {
            cart: {
                type: Array
            },
            courses: {
                type: Array
            }
        },
        data() {
            return {
                checkout: {
                    name: "",
                    phone: ""
                }
            };
        },

        methods: {
            onItemTap(event) {
                this.$emit("removeCourse", event.item);
            },
            submit() {
                fetch("https://individual2cw.herokuapp.com/collection/order", {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json"
                        },
                        mode: "cors",
                        cache: "no-store",
                        body: JSON.stringify(this.checkout)
                    })
                    .then(response => response.json())
                    .then(responseJSON => {})
                    .catch(error => {
                        console.log(error);
                    });
                alert("you have submitted your order");
                this.cart.length = 0;
            }
        }
    };
</script>
<style>
</style>
