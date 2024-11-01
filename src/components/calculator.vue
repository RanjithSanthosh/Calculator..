<template>
    <div class="bg-gray-300 flex justify-center items-center h-screen">
        
        <div class="bg-black text-white  grid grid-cols-4 gap-3 p-5 rounded-md ">
            <input v-model="displayval" type="text" class=" mb-2 col-span-4 text-right text-2xl bg-gray-800 text-white p-3 rounded-md focus:outline-none " placeholder="0" disabled />
            <div @click="clear()" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >AC</div>
            <div @click="back()" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >B</div>
            <div @click="appendval('%')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >%</div>
            <div @click="appendval('/')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >/</div>

            <div @click="appendval('7')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >7</div>
            <div @click="appendval('8')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >8</div>
            <div @click="appendval('9')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >9</div>
            <div @click="appendval('*')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >*</div>

            <div @click="appendval('4')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >4</div>
            <div @click="appendval('5')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >5</div>
            <div @click="appendval('6')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >6</div>
            <div @click="appendval('-')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >-</div>

            <div @click="appendval('1')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >1</div>
            <div @click="appendval('2')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >2</div>
            <div @click="appendval('3')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >3</div>
            <div @click="appendval('+')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >+</div>

            <div class=""></div>
            <div @click="appendval('0')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >0</div>
            <div @click="appendval('.')" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >.</div>
            <div @click="calculate()" class="bg-white text-black w-9 h-9 flex justify-center items-center rounded-md hover:cursor-pointer hover:bg-blue-800" >=</div>
        </div>
    </div>
</template>

<!-- <script>
export default {
    data(){
        return{
            displayval :'0',
        };
    },
    methods:{
        appendval(num){
            this.displayval+=num;
        },
        clear(){
            this.displayval='0';
        },
        back(){
            this.displayval=this.displayval.slice(0,-1) || '0';
        },
        calculate(){
            try {
                this.displayval = eval(this.displayval).toString(); // Corrected here
            } catch {
                this.displayval = 'Error'; // Make sure this matches the variable name
            }
        },
    },
}
</script> -->

<script>
export default {
    data() {
        return {
            displayval: '0',
        };
    },
    methods: {
        appendval(num) {
            
            const lastChar = this.displayval[this.displayval.length - 1];
            const operators = "+-*/";
            
           
            if (operators.includes(lastChar) && operators.includes(num)) {
                return;
            }

            
            this.displayval = this.displayval === '0' ? num : this.displayval + num;
        },
        clear() {
            this.displayval = '0';
        },
        back() {
            this.displayval = this.displayval.slice(0, -1) || '0';
        },
        calculate() {
            try {
                const sanitizedInput = this.displayval.replace(/\s/g, ''); 
                
                
                if (/^[\d+\-*/().]+$/.test(sanitizedInput)) {
                    this.displayval = eval(sanitizedInput).toString(); 
                } else {
                    throw new Error("Invalid input");
                }
            } catch (error) {
                this.displayval = 'Error';
            }
        },
    },
}
</script>

<style scoped>

</style>
