<script>
    export default { 
        // Add Code Here to complete the task
        // Note: DO NOT USE "eval()". In security, "eval" is considered "evil"!!!
        data() {
            return {
                x: '', //set initial vvalue as empty and to get the input value
                y: '', // same as x
                operators: ['+','-','*','/','%'], // data to populate the dropdown
                selectedOp: '', // the operator that we take in cos v-model bind
            }
        },
        computed: {
            result() {
                const x = this.x;
                const y = this.y;
                // since no eval(), manually do operations
                switch(this.selectedOp){
                    case '+': return x+y;
                    case '-': return x-y; 
                    case '*': return x*y;
                    case '/': return y !== 0 ? x / y : 'Error'
                    case '%': return y !== 0 ? x % y : 'Error'
                }
            }
        }
    }
</script>

<template>
    <p>x <input v-model.number="x"></p>
    <select v-model="selectedOp">
        <option v-for="op in operators" >{{ op }}</option>
    </select>
    <p>y <input v-model.number="y"></p>
    
    <p>---------------------</p>

    <p>= {{result}}</p>
</template>

<style scoped>
    p, input { font-family: monospace; }
    p { white-space: pre; }

</style>
