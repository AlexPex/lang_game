<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import millionaire from './components/millionaire.vue'
import { onMounted } from 'vue'
//dev temporar settings
onMounted(() => {
  $('#app_header').removeClass('text-primary').addClass('text-white');
  $('#app_header').addClass('text-white');
  $('#app_task').text('Игра "Кто хочет чтать миллионером?"').addClass('text-white');
})

function runGame(event) {
  console.log($(event.target).parent().data('game'));
  $('.list_of_games').fadeOut();
  switch ($(event.target).parent().data('game')) {
    case 'millionaire':
      $('#app_header').removeClass('text-primary').addClass('text-white');
      $('#app_header').addClass('text-white');
      $('#app_task').text('Игра "Кто хочет чтать миллионером?"').addClass('text-white');
      $('#game_millionaire').removeClass('d-none').fadeInt();
      break;
  
    default:
      break;
  }
}

</script>

<template>
  <h1 class="text-center text-primary" id="app_header">Игры по лингвистике</h1>
  <h2 class="text-center" id="app_task">Выберите игру</h2>
  <div class="row list_of_games d-none">
    <div class="col-6">
      <div class="game text-center" @click="runGame" data-game="millionaire">
        <img src="../public/img/orig.png" class="img-fluid rounded " alt="">
        <p>Нажми на картинку чтобы сыграть</p>
      </div>
    </div>
    <div class="col-6">
      <div class="game text-center" @click="runGame" data-game="millionaire">
        <img src="../public/img/orig.png" class="img-fluid rounded " alt="">
        <p>Нажми на картинку чтобы сыграть</p>
      </div>
    </div>
  </div>
  <div class="row list_of_games d-none">
    <div class="col-6">
      <div class="game text-center" @click="runGame" data-game="millionaire">
        <img src="../public/img/orig.png" class="img-fluid rounded " alt="">
        <p>Нажми на картинку чтобы сыграть</p>
      </div>
    </div>
    <div class="col-6">
      <div class="game text-center" @click="runGame" data-game="millionaire">
        <img src="../public/img/orig.png" class="img-fluid rounded " alt="">
        <p>Нажми на картинку чтобы сыграть</p>
      </div>
    </div>
  </div>

  <millionaire msg="Vite + Vue" />
  <!-- <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="../public/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <p @click="test">Click me</p>
  <HelloWorld msg="Vite + Vue" /> -->
</template>
