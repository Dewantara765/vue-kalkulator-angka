<script setup>
import {ref} from 'vue'

const teks = ref("")
const kalkulasi = ref(false)


function inputAngka (value) {
  if(this.kalkulasi){
    this.teks = value
    this.kalkulasi = false
  }else{
     this.teks += value
  }

}

function bersihkan () {
  this.teks = ''
  this.kalkulasi = false
}

function bersihkanEntri (){
  if (this.teks && this.teks.length > 0) {
        this.teks = this.teks.slice(0, -1);
        if (this.teks.length === 0) {
          this.bersihkan();
        }
      } else {
        this.bersihkan();
      }
}

function inputOperator(operator){
  if (/[+*/-]$/.test(this.teks)) {
        this.teks = this.teks.slice(0, -1) + operator;
      } else {
        // Otherwise, add the new operator
        this.teks += operator;
      }
      this.kalkulasi = false;
}

function hitung() {
      try {
        let hasilOperasi = eval(this.teks.
            replace(/(^|[^0-9])0+(\d+)/g, '$1$2'));
        if (hasilOperasi === Infinity ||
            hasilOperasi === -Infinity) {
          throw new Error('Error tidak bisa dibagi nol');
        }
        this.teks = Number.isFinite(evaluatedResult)
                      ? evaluatedResult : 'Error';
        this.kalkulasi = true;
        // Set flag to true after calculation
      } catch (error) {
        if (error.message === 'Error tidak bisa dibagi nol') {
          this.teks = 'Error: Tidak bisa dibagi nol';
        } else {
          this.teks = 'Error';
        }
      }
}
</script>

<template>

  <main>
    <div class="container">
      <input type="text" name="inputAngka" id="inputAngka" class="input-angka" v-model="teks">
      <div class="tempat-angka">
        <button class="btn-angka" @click="inputAngka('1')">1</button>
        <button class="btn-angka" @click="inputAngka('2')">2</button>
        <button class="btn-angka" @click="inputAngka('3')">3</button>
        <button class="btn-angka" @click="inputAngka('4')">4</button>
        <button class="btn-angka" @click="inputAngka('5')">5</button>
        <button class="btn-angka" @click="inputAngka('6')">6</button>
        <button class="btn-angka" @click="inputAngka('7')">7</button>
        <button class="btn-angka" @click="inputAngka('8')">8</button>
        <button class="btn-angka" @click="inputAngka('9')">9</button>
        <button class="btn-angka" @click="inputAngka('0')">0</button>
        <button class="btn-angka" @click="inputAngka('.')">.</button>
        <button class="btn-angka" @click="inputOperator('+')">+</button>
        <button class="btn-angka" @click="inputOperator('-')">-</button>
        <button class="btn-angka" @click="inputOperator('*')">*</button>
        <button class="btn-angka" @click="inputOperator('/')">/</button>
        <button class="btn-angka" @click="bersihkan()">C</button>
        <button class="btn-angka" @click="bersihkanEntri()">CE</button>
        <button class="btn-angka" @click="hitung()">=</button>
      </div>
      

    </div>
 
  </main>
</template>

<style scoped>
.container{
  width: 300px;
  height: 600px;
  background-color: rgb(52, 192, 235);
  padding: 20px 30px;
  
}

.input-angka{
  font-size: 16px;
  font-family:Arial, Helvetica, sans-serif;
  margin: 20px;
  padding : 10px;
}

.tempat-angka{
  width : 80%;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  margin: 20px;

}

.btn-angka{
  font-size: 16px;
  font-family: Arial, Helvetica, sans-serif;
  margin: 5px;
  background-color: #ff0000;
  color: white;
  padding: 10px;
  width: 50px;
  border : none;
  border-radius : 5px;
  cursor: pointer;
}
</style>
