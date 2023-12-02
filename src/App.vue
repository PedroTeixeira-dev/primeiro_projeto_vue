<script setup>
import {reactive} from 'vue';


const nome = 'Pedro Teixeira'

const meuObjeto = {
  nome: 'pedro',
  filmeFavorito: 'SW'
}

function dizOla() {
  return `O fime favorito do ${nome} e ${meuObjeto.filmeFavorito}`
}

const enderecoImagemBatman = 'https://portalperifacon.com/wp-content/uploads/2022/09/fsdfsdfsdfsd.jpg'

const enderecoImagemSuper = 'https://t.ctcdn.com.br/sS0dqwq3BA9nGFigIH26q8YHOgI=/640x360/smart/i677638.jpeg'

const botaoDesabilitado = true

const gostaBatman = true
const gostaSuper = true

const estaAutorizado = false

// let contador = 0

const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['Gian', 'Paulo', 'Pedro', 'Mel'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador ++
}

function decrementar() {
  estado.contador --
}

function alteraEmail(evento) {
  estado.email = evento.target.value
}

function mostraSaldoFuturo(){
  const {saldo, transferindo} = estado
  return saldo - transferindo
}

function validaTranferencia() {
  const {saldo, transferindo} = estado
  return saldo >= transferindo
}

function cadastraNome() {
  if (estado.nomeAInserir.length >= 3){
  estado.nomes.push(estado.nomeAInserir)
} else {
  alert("Digite mais caracteres")
}
}

</script>

<template>
<h1>{{dizOla()}}</h1>
<img v-if="gostaBatman" v-bind:src="enderecoImagemBatman" alt="">

<img v-else-if="gostaSuper" :src="enderecoImagemSuper" alt="">

<h2 v-else>Nao curte herois da DC</h2>

<h1 v-if="estaAutorizado">Bem vindo</h1>
<h1 v-else>Acesso negado</h1>


<button :disabled="botaoDesabilitado">Enviar Mensagem</button>

<br/>
<hr/>

{{ estado.contador }}

<button @click="incrementar" type="button">+</button>
<button @click="decrementar" type="button">-</button>

<br/>
<hr/>

{{ estado.email }}

<br/>

<input type="email" @keyup="alteraEmail">

<br/>
<hr/>

Saldo: {{ estado.saldo }} <br/>
Transferindo: {{ estado.transferindo }} <br/>
Saldo apos transferencia: {{ mostraSaldoFuturo() }} <br/>
<input :class="{ invalido: !validaTranferencia() }" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
<br/>
<button type="button" v-if="validaTranferencia()" >Transferir</button>
<span v-else>Valor maior que o saldo disponivel</span>

<br/>
<hr/>

<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>
<input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text" placeholder="Digite um novo nome">
<br/>
<button @click="cadastraNome()" type="button">Cadastrar nome</button>
<br/>
<button type="button">Deletar nomes</button>

</template>

<style scoped>
img {
  max-width: 400px;
}

.invalido {
  outline-color: red;
  border-color: red;
}
</style>


<!-- // http://localhost:5173/ -->