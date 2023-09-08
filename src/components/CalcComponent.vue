<template>
    <div>
        <div class="calc">
            <!-- <input type="text" class="input" v-model="result">
            <button
            @click="addButton(num)"
            v-for="num in nums" :key="num.id"
                >{{ num }}
            </button>
            <button @click="addButton(tab)"
            v-for="tab in tabs" :key="tab.id"
                >{{ tab }}
            </button>
            <button @click="calcResult">=</button>
            <button @click="reset" class="reset">reset</button> -->
            <input type="text" v-model="operand1">
            <input type="text" v-model="operand2">
            {{ result }}
            <!-- <button @click="calcAllResult('+')">+</button>
            <button @click="calcAllResult('-')">-</button>
            <button @click="calcAllResult('/')">/</button>
            <button @click="calcAllResult('*')">*</button> -->
            <button @click="calcAllResult(operation)" v-for="operation in operations" :key="operation.id">
                {{ operation }}
            </button>
            
            <div>
                <!-- {{ error }} -->
                    <div v-show="error">
                        {{ error }}
                    </div>
            </div>
            <div>
                <template v-if="result < 0">Negative number</template>
            </div>
            <div>
                <template v-if="result >= 0 && result <= 100">Positive number below 101</template>
            </div>
            <div>
                <template v-if="result > 100">Positive number greater than 100</template>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'CalcComponent',

        data(){
            return{
                // result: '',
                // nums:[1,2,3,4,5,6,7,8,9,0],
                // tabs:['-', '+', '*', '/'],
                operand1: 0,
                operand2: 0,
                result: 0,
                operations:['+', '-', '*', '/'],
                error: '',
            };
        },

        methods:{
            // addButton(char){
            //     this.result = this.result.toString();
            //     this.result += char;
            // },

            // calcResult(){
            //     this.result = eval(this.result);
            // },

            // reset(){
            //     this.result = '';
            // }

            add(){
                this.result = Number(this.operand1) + Number(this.operand2);
            },

            minus(){
                this.result = Number(this.operand1) - Number(this.operand2);
            },

            multi(){
                this.result = Number(this.operand1) * Number(this.operand2);
            },

            divide(){
                // this.result = Number(this.operand1) / Number(this.operand2);

                const {operand1, operand2} = this;
                if (operand2 == 0) {
                    this.error = "can't divide by 0";
                } else {
                    this.result = operand1 / operand2;
                }
            },

            calcAllResult(operation){
                this.error = '';
                switch (operation) {
                    case '+':
                        this.add();
                        break;
                    case '-':
                        this.minus();
                        break;
                    case '*':
                        this.multi();
                        break;
                    case '/':
                        this.divide();
                        break;
                
                    default:
                        break;
                }
            }
        },
        
    }
</script>

<style lang="css" scoped>

    .calc{
        display: grid;
        grid-template-columns: repeat(3,150px);
        justify-content: center;
        padding-top: 48px;
        padding-bottom: 48px;
    }

    .input{
        grid-column: 1 / -1;
        text-align: right;
    }

    .reset{
        grid-column: 1 / -1;
    }
</style>