<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                itemToAdd: ''
            }
        },
        methods: {
            addItem() {
                if (this.itemToAdd.length!=0){
                    this.items.push(this.itemToAdd)
                    }
                else {
                    alert('Add Something')
                }
            },
            delItem(index) {
                this.items.splice(index, 1)
            }
        }
    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
   <ul>
    <!-- add the index as well so i can remove from from array by index -->
    <li v-for="(item,index) in items" :key="index">{{ item }}<button @click="delItem(index)">Delete!</button></li>
   </ul>

   <input v-model="itemToAdd"><button @click=addItem>Add!</button>
</template>
