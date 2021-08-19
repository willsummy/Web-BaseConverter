<template>
  <div>
      <h3>Integral Converter</h3>

      <form class="UserInput">
            <input type="text" placeHolder="Enter A Number" v-model="initialNum" v-on:submit.prevent="convertNum">
            <label for="initialBase">Starting Base</label>
            <select name="initialBase" id="initialBase" v-model="initialBase">
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
                <option value="6">6</option>
                <option value="7">7</option>
                <option value="8">8</option>
                <option value="9">9</option>
                <option default value="10">10</option>
                <option value="11">11</option>
                <option value="12">12</option>
                <option value="13">13</option>
                <option value="14">14</option>
                <option value="15">15</option>
                <option value="16">16</option>
                <option value="17">17</option>
                <option value="18">18</option>
                <option value="19">19</option>
                <option value="20">20</option>
                <option value="21">21</option>
                <option value="22">22</option>
                <option value="23">23</option>
                <option value="24">24</option>
                <option value="25">25</option>
                <option value="26">26</option>
                <option value="27">27</option>
                <option value="28">28</option>
                <option value="29">29</option>
                <option value="30">30</option>
                <option value="31">31</option>
                <option value="32">32</option>
                <option value="33">33</option>
                <option value="34">34</option>
                <option value="35">35</option>
                <option value="36">36</option>
            </select>
            <label for="finalBase">Final Base</label>
            <select name="finalBase" id="finalBase" v-model="finalBase">
                <option default value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
                <option value="6">6</option>
                <option value="7">7</option>
                <option value="8">8</option>
                <option value="9">9</option>
                <option value="10">10</option>
                <option value="11">11</option>
                <option value="12">12</option>
                <option value="13">13</option>
                <option value="14">14</option>
                <option value="15">15</option>
                <option value="16">16</option>
                <option value="17">17</option>
                <option value="18">18</option>
                <option value="19">19</option>
                <option value="20">20</option>
                <option value="21">21</option>
                <option value="22">22</option>
                <option value="23">23</option>
                <option value="24">24</option>
                <option value="25">25</option>
                <option value="26">26</option>
                <option value="27">27</option>
                <option value="28">28</option>
                <option value="29">29</option>
                <option value="30">30</option>
                <option value="31">31</option>
                <option value="32">32</option>
                <option value="33">33</option>
                <option value="34">34</option>
                <option value="35">35</option>
                <option value="36">36</option>
            </select>
            <button id="clearBtn" v-on:click.prevent="clearForm">Clear</button>
            <button id="convertBtn" v-on:click.prevent="convertNum">Convert</button>
      </form>
      <h4>Output: {{finalNum}}</h4>
  </div>
</template>

<script>
export default {
    name: 'integral-converter',
    data() {
        return {
            initialNum: null,
            finalNum: null,
            initialBase: 10,
            finalBase: 2
        }
    },
    methods: {
        clearForm() {
            this.initialNum = null
            this.finalNum = null
            this.initialBase = 10
            this.finalBase = 2
        },
        convertNum() {
            if (this.validateUserInput(this.initialNum)) {
                if (this.initialNum == null) {
                    this.finalNum = "Please Enter An Integer"
                    return
                }
                let sum = 0;
                let integral = this.initialNum
                let newNumber = '';
                
                for (let i = integral.length-1, j=0; i > -1; i--, j++) {
                    let currentChar = integral.slice(i, i+1)
                    let currentValue = this.$store.state.toDecimal[currentChar.toUpperCase()]
                    sum += currentValue * Math.pow(parseInt(this.initialBase), j);
                }

                while(sum > 0) {
                    let remainder = sum % this.finalBase;
                    let newChar = this.$store.state.fromDecimal[remainder];
                    newNumber = newChar + newNumber;
                    sum = Math.floor(sum/this.finalBase)
                }

                this.finalNum = newNumber;
            } else this.finalNum = "Please use correct notation"
            
        },
        validateUserInput(input) {
            for (let i = 0; i < input.length; i++) {
                if (this.initialBase <= this.$store.state.toDecimal[input.charAt(i)]) {
                    return false
                }

            }
            return true
        }
    }

}
</script>

<style>

</style>