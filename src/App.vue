<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script setup>
import HelloWorld from './components/HelloWorld.vue'
import BlowFish from 'blowfish';
import aesjs from 'aes-js'
import CryptoJS  from 'crypto-js';

const bf = new BlowFish('sass');
const encrypted = bf.encrypt('danila');
let decrypted = bf.decrypt(encrypted);
console.log(encrypted, decrypted, 'blowFish');
var data = [{id: 1}, {id: 2}]

// Encrypt
var ciphertext = CryptoJS.DES.encrypt(JSON.stringify(data), 'secret key 123').toString();
console.log(ciphertext, 'ciphertText')
// An example 128-bit key (16 bytes * 8 bits/byte = 128 bits)
var key = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 ];
 
// Convert text to bytes
var text = 'Text may be any length you wish, no padding is required.';
var textBytes = aesjs.utils.utf8.toBytes(text);
 
// The counter is optional, and if omitted will begin at 1
var aesCtr = new aesjs.ModeOfOperation.ctr(key, new aesjs.Counter(5));
var encryptedBytes = aesCtr.encrypt(textBytes);
 
// To print or store the binary data, you may convert it to hex
var encryptedHex = aesjs.utils.hex.fromBytes(encryptedBytes);
console.log(encryptedHex);
// "a338eda3874ed884b6199150d36f49988c90f5c47fe7792b0cf8c7f77eeffd87
//  ea145b73e82aefcf2076f881c88879e4e25b1d7b24ba2788"
 
// When ready to decrypt the hex string, convert it back to bytes
encryptedBytes = aesjs.utils.hex.toBytes(encryptedHex);
 
// The counter mode of operation maintains internal state, so to
// decrypt a new instance must be instantiated.
aesCtr = new aesjs.ModeOfOperation.ctr(key, new aesjs.Counter(5));
var decryptedBytes = aesCtr.decrypt(encryptedBytes);
 
// Convert our bytes back into text
var decryptedText = aesjs.utils.utf8.fromBytes(decryptedBytes);
console.log(decryptedText);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
