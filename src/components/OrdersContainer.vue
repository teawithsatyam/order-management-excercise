<script>
import OrderItem from './OrderItem.vue'
    export default {
        components : {
            'order-item' : OrderItem
        },
         data(){
            return{
                order : []
            }
        },
        computed:{
            getOrders(){
                return this.$store.state.orders
            }
        },
        mounted(){
            this.$http.get('http://18.217.149.238:3000/orders').then(response=>{
                this.$store.dispatch('mutateOrders',response.body.response)
            })
        },
        beforeMount() {
            if(localStorage._token === ""){
            this.$router.push('/login')
        }
  }
    }
</script>

<template>
    <div class="order_container" >
        <!-- Title -->
        <div class="title">
        Orders
        </div>
        <!-- Products -->
        <div class="orders">
            <order-item v-for="order in getOrders" v-bind:key = "order._id" :order="order"/> 
        </div>
    </div>
</template>



<style lang="scss" scoped>
.order_container {
    width: 90%;
    max-width : 915px;
    height: 423px;
    margin: 25px auto;
    background: #FFFFFF;
    box-shadow: 1px 2px 3px 0px rgba(0,0,0,0.10);
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    .title {
        height: 60px;
        border-bottom: 1px solid #E1E8EE;
        padding: 20px 30px;
        color: #5E6977;
        font-size: 18px;
        font-weight: 400;
    }
    .orders{
        padding: 10px;
    }
}
@media (max-width: 800px) {
    .shopping-cart {
        width: 80%;
        height: auto;
        overflow: hidden;
    }
}
</style>