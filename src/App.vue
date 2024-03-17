<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import millionaire from './components/millionaire.vue'
import field_of_shame from './components/field_of_shame.vue'
import { onMounted } from 'vue'

let game_shame = { score: 0 };
//dev temporar settings
onMounted(() => {
    // $('#app_header').removeClass('text-primary').addClass('text-white');
    // $('#app_header').addClass('text-white');
    // $('#app_task').text('Игра "Определи поле состояния"').addClass('text-white');
    // $('#app_task').append('<button type="button" class="btn btn-outline-light ms-2" id="goToMenu">Перейти в меню</button>');
    // $('body').addClass('background_field_of_shame');
   
});

function onlyUnique(value, index, array) {
    return array.indexOf(value) === index;
}
function runDrag_Drop(dragElementId = null) {
    if (dragElementId == null) return;

    var dragElement = document.getElementById(dragElementId);
    var dropZone = document.getElementById('game_field_of_shame_drop');


    dragElement.onmousedown = function (e) { // 1. отследить нажатие

        if (!$('#' + dragElementId).prop('draggable')) {
            return;
        }
        // подготовить к перемещению
        // 2. разместить на том же месте, но в абсолютных координатах
        dragElement.style.position = 'absolute';
        moveAt(e);
        // переместим в body, чтобы мяч был точно не внутри position:relative
        // document.body.appendChild(dragElement);
        dropZone.appendChild(dragElement);
        if (dragElementId === 'core_circle') {
            dragElement.style.zIndex = 1000; // показывать мяч над другими элементами
        } else {
            dragElement.style.zIndex = 800; // показывать мяч над другими элементами
        }

        // передвинуть мяч под координаты курсора
        // и сдвинуть на половину ширины/высоты для центрирования
        function moveAt(e) {
            if (e.pageY >= $('#drag_container').position().top &&
                e.pageY <= $('#drag_container').position().top + $('#drag_container').height()) {
                // console.log(e.pageX, dragElement.offsetWidth);
                // console.log(e.pageY, dragElement.offsetHeight);
                dragElement.style.left = e.pageX - dragElement.offsetWidth / 2 + 'px';
                dragElement.style.top = e.pageY - dragElement.offsetHeight / 2 + 'px';
            }

            // dragElement.style.left = e.pageX - dragElement.offsetWidth / 2 + 'px';
            // dragElement.style.top = e.pageY - dragElement.offsetHeight / 2 + 'px';
        }

        // 3, перемещать по экрану
        document.onmousemove = function (e) {
            if (!$('#' + dragElementId).prop('draggable')) {
                return;
            }
            moveAt(e);
        }

        // 4. отследить окончание переноса
        dragElement.onmouseup = function () {
            document.onmousemove = null;
            dragElement.onmouseup = null;
        }
        dragElement.ondragstart = function () {
            return false;
        };
    }
}

function showMenu(game, background_class, score = null) {
    $('#' + game).addClass('d-none').fadeOut();
    $('body').removeClass(background_class);
    if (score != null || score > 0) {
        $('#' + game + '_score').text('Набрано: ' + score + ' баллов').removeClass('invisible');
    }
    $('#app_header').removeClass('text-white').addClass('text-primary');
    $('#app_task').text('Выберите игру');
    $('#app_task').removeClass('text-white');
    $('.list_of_games').fadeIn();
}

function runGame(event) {
    console.log($(event.target).parent().data('game'));
    $('.list_of_games').fadeOut();
    switch ($(event.target).parent().data('game')) {
        case 'millionaire':
            $('#app_header').removeClass('text-primary').addClass('text-white');
            $('#app_header').addClass('text-white');
            $('body').addClass('background_millionaire');
            $('#app_task').text('Игра "Кто хочет чтать миллионером?"').addClass('text-white');
            $('#game_millionaire').removeClass('d-none').fadeIn();
            $('#app_task').append('<button type="button" class="btn btn-outline-light ms-2" id="goToMenu">Перейти в меню</button>');
            setTimeout(() => {
                $('#goToMenu').click(() => {
                    showMenu('game_millionaire', 'background_millionaire');
                });
            }, 500);
            break;
        case 'field_of_shame':
            $('#app_header').removeClass('text-primary').addClass('text-white');
            $('#app_header').addClass('text-white');
            $('body').addClass('background_field_of_shame');
            $('#app_task').text('Игра "Определи поле состояния"').addClass('text-white');
            $('#app_task').append('<button type="button" class="btn btn-outline-light ms-2" id="goToMenu">Перейти в меню</button>');
            $('#game_field_of_shame').removeClass('d-none').fadeIn();
            setTimeout(() => {
                $('#goToMenu').click(() => {
                    showMenu('game_field_of_shame', 'background_field_of_shame', game_shame.score);
                });
                $('#start_movement').click(() => {
                    $('#toast .toast-body').text('Вы можете начать перетаскивание.');
                    $('#toast .toast-header .bi-bell-fill').removeClass('text-danger').addClass('text-success');
                    $('.toast').toast('show');
                    $('#core_circle').prop('draggable', true);
                    $('#external_circle').prop('draggable', true);
                    runDrag_Drop('core_circle');
                    runDrag_Drop('external_circle');
                    $('#start_movement').attr('disabled', 'disabled');
                });

                $('#end_movement').click(() => {
                    $('#toast .toast-body').text('Перетаскивание отключено');
                    $('#toast .toast-header .bi-bell-fill').removeClass('text-success').addClass('text-danger');
                    $('.toast').toast('show');
                    $('#core_circle').prop('draggable', false);
                    $('#external_circle').prop('draggable', false);

                    const pos = $('#core_circle').position();
                    const posContainer = $('#game_field_of_shame_drop').position();
                    $('#game_field_of_shame_drop').css('position', 'relative');

                    $('#core_circle').css({
                        // position: 'relative',
                        top: pos.top - posContainer.top,
                        left: pos.left - posContainer.left,
                    });
                    const pos2 = $('#external_circle').position();
                    $('#external_circle').css({
                        // position: 'relative',
                        top: pos2.top - posContainer.top,
                        left: pos2.left - posContainer.left,
                    });
                    $('#game_field_of_shame_check').removeClass('invisible');
                    $('#end_movement').attr('disabled', 'disabled');
                });
                setTimeout(() => {
                    $('#game_field_of_shame_check').click(() => {
                        const core = $('#core_cicle_input').val().trim().toLowerCase();
                        const external = $('#external_cicle_input').val().trim().toLowerCase();
                        //tests
                        if (!core.length || !external.length) {
                            alert('Введите текст в оба поля');
                            return;
                        }
                        if (core.length) {
                            $('#core_circle').wrap('<p class="core_container"></p>');
                            // main circle
                            let pos = $('#core_circle').position();
                            $('.core_container').css({ top: pos.top, left: pos.left });
                            $('#core_circle').css({ top: 0, left: 0 });
                            $('.core_container').append(`<p class="centered">${core}</p>`);
                        }

                        if (external.length) {
                            //external circle
                            $('#external_circle').wrap('<p class="external_container"></p>');
                            let pos2 = $('#external_circle').position();
                            $('.external_container').css({ top: pos2.top, left: pos2.left });
                            $('#external_circle').css({ top: 0, left: 0 });
                            $('.external_container').append(`<p class="bottom-left">${external}</p>`);
                            pos2 = $('.external_container').position();
                            $('.core_container').css({ top: -1 * ((pos2.top / 2 - 105)) });
                        }
                        $('#game_field_of_shame_check').addClass('invisible');
                        //checks
                        let uniqueWords = core.split(',').filter(onlyUnique);
                        uniqueWords.forEach(word => {
                            word = word.trim();
                            console.log(word);
                            if (word === 'стыдно' || word === 'стыд' || word === 'стыдитесь') {
                                game_shame.score += 2;
                            } else {
                                game_shame.score -= 0.2;
                            }
                        });
                        uniqueWords = external.split(',').filter(onlyUnique);
                        uniqueWords.forEach(word => {
                            word = word.trim();
                            console.log(word);
                            if (word === 'неловко' || word === 'смущенно' || word.includes('позор')) {
                                game_shame.score += 2;
                            } else {
                                game_shame.score -= 0.2;
                            }
                        });
                        setTimeout(() => {
                            alert('Вы набрали ' + game_shame.score + ' баллов из 12');
                        }, 500);
                    });
                }, 900);
            }, 500);
            break;

        default:
            break;
    }
}

</script>

<template>
    <h1 class="text-center text-primary" id="app_header">Игры по лингвистике</h1>
    <h2 class="text-center" id="app_task">Выберите игру</h2>
    <div class="row list_of_games">
        <div class="col-6">
            <div class="game text-center" @click="runGame" data-game="millionaire">
                <img src="../public/img/orig.png" class="img-fluid rounded " alt="">
                <p>Нажми на картинку чтобы сыграть <span class="alert alert-info py-0 invisible" role="alert"
                        id="millionaire_score"></span></p>
            </div>
        </div>
        <div class="col-6">
            <div class="game text-center position-relative" @click="runGame" data-game="field_of_shame">
                <img src="../public/img/background-3.webp" class="img-fluid rounded " alt="">
                <h3 class="position-absolute top-50 start-0">Определи поле состояния</h3>
                <p>Нажми на картинку чтобы сыграть <span class="alert alert-info  py-0 invisible" role="alert"
                        id="field_of_shame_score"></span></p>
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
    <field_of_shame />
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
