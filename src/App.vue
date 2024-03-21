<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import millionaire from './components/millionaire.vue'
import field_of_shame from './components/field_of_shame.vue'
import extra_circle from './components/extra_circle.vue'
import { onMounted } from 'vue'
const isPublished = true;
let path = '../public'
if (isPublished) {
    path = '../';
}
let game_shame = { score: 0 };
let game_millionaire = { score: 0, answers: [], previous_score: 0 };
let game_extra_circle = {
    score: 0, answers: [
        'от радости, волнения и стыда', 'страх', "жалости", "заплакала слезами", "преисполнена отчаяния, стыда, унижения,",
        "виновата", "побежденного", "поспешно отвернувшись,", "ушел", "высшей степени хохота.", "погибель",
        "измена."
] };
let background_music = new Audio(path + '/audio/base.mp3');
let correct_answer_music = new Audio(path + '/audio/correct_answer.mp3');
let wrong_answer_music = new Audio(path + '/audio/wrong_answer.mp3');
let ending_music = new Audio(path + '/audio/finish.mp3');
let jquery_ui_path = path + '/js/jquery-ui.min.js';

//dev temporar settings
onMounted(() => {
    // $('#app_header').removeClass('text-primary').addClass('text-white');
    // $('#app_header').addClass('text-white');
    // $('#app_task').text('Игра "Определи поле состояния"').addClass('text-white');
    // $('#app_task').append('<button type="button" class="btn btn-outline-light ms-2" id="goToMenu">Перейти в меню</button>');
    // $('body').addClass('background_field_of_shame');
    $('body[class="background"]').removeClass();
    $('body').append(`<script src="${jquery_ui_path}" id="jq_ui">`);
   
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
    background_music.pause();
    correct_answer_music.pause();
    wrong_answer_music.pause();
    ending_music.pause();
    $('#' + game).addClass('d-none').fadeOut();
    $('body').removeClass(background_class);
    if (score != null || score > 0) {
        console.log('#' + game + '_score');
        $('#' + game + '_score').text('Набрано: ' + score + ' баллов').removeClass('invisible');
    }
    $('#app_header').removeClass('text-white').addClass('text-primary');
    $('#app_task').text('Выберите игру');
    $('#app_task').removeClass('text-white');
    $('.list_of_games').fadeIn();
}

// this function changes button state according to the answer- green or red
function changeButtonStatus(question, element_id, status = 'success') {
    $(`#${element_id} .btn-outline-dark`).each((index, btn) => {
        if ($(btn).text().trim().startsWith(question.answer + '. ')) {
            console.log('yes');
            if (status === 'success') {
                $(btn).toggleClass('btn-outline-dark btn-outline-success');
            } else {
                $(btn).toggleClass('btn-outline-dark btn-outline-danger');
            }

        }

    });
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
                    showMenu('game_millionaire', 'background_millionaire', game_millionaire.score);
                });
                //logic of the game
                //sound
                
                background_music.play();
                //handle what block of question will appear next
                $('.game_millionaire_next').click(function () {
                    
                    let id_question = $(this).parents('.card').attr('id').split('_q');
                    $('#' + $(this).parents('.card').attr('id')).fadeOut();
                    let nextQuestionId = '#' + id_question[0] + '_q' + (parseInt(id_question[1]) + 1);
                    if (nextQuestionId === '#game_millionaire_q9') {
                        ending_music.play();
                        $('#game_millionaire_score1').text(game_millionaire.score);
                    } else {
                        background_music.play();
                    }
                    console.log(nextQuestionId);
                    $(nextQuestionId).removeClass('d-none').fadeIn();
                });
                // save user answers by clicking the button
                $('#game_millionaire .btn-outline-dark').click(function () {
                    if (!$(this).hasClass('active')) {
                        $(this).addClass('active');
                    }
                    let question_id = $(this).parents('.card').attr('id');
                    let answer = $(this).text().split('.')[0].trim();
                
                    if (question_id.length > 5 && answer.length === 1) {
                        game_millionaire.answers.push({
                            id: question_id,
                            answer: answer
                        });
                    } else {
                        alert('Ошибка! Не могу понять ответ.');
                    }
                });
                $('.game_millionaire_answer').click(function () {
                    background_music.pause();
                    background_music.load();
                    let question_id = $(this).parents('.card').attr('id');
                    let answers = game_millionaire.answers.filter((el) => {
                        return el.id === question_id;
                    });
                    $(this).attr('disabled', 'disabled');
                    $(this).prev().removeClass('invisible');

                    console.log(answers);
                    switch (question_id) {
                        case "game_millionaire_q1":
                            answers.forEach(element => {
                                if (element.answer === 'G' || element.answer === 'C') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q2":
                            answers.forEach(element => {
                                if (element.answer === 'F') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q3":
                            answers.forEach(element => {
                                if (element.answer === 'G') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q4":
                            answers.forEach(element => {
                                if (element.answer === 'A') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q5":
                            answers.forEach(element => {
                                if (element.answer === 'A') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q6":
                            answers.forEach(element => {
                                if (element.answer === 'A') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q7":
                            answers.forEach(element => {
                                if (element.answer === 'C') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                        case "game_millionaire_q8":
                            answers.forEach(element => {
                                if (element.answer === 'C' || element.answer === 'A') {
                                    game_millionaire.score += 1;
                                    changeButtonStatus(element, element.id);
                                } else {
                                    game_millionaire.score -= 0.1;
                                    changeButtonStatus(element, element.id, 'danger');
                                }
                            });
                            break;
                    }
                    if (game_millionaire.score > game_millionaire.previous_score) {
                        correct_answer_music.play();
                        setTimeout(() => {
                            correct_answer_music.pause();
                            correct_answer_music.load();
                        }, 5000);
                    } else {
                        wrong_answer_music.play();
                        setTimeout(() => {
                            wrong_answer_music.pause();
                            wrong_answer_music.load();
                        }, 5000);
                    }
                    game_millionaire.previous_score = game_millionaire.score
                    console.log(game_millionaire);
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
        case 'extra_circle':
            $('#app_header').removeClass('text-primary').addClass('text-white');
            $('#app_header').addClass('text-white');
            $('body').addClass('background_field_of_shame');
            $('#app_task').text('Игра "Периферия семантического поля стыд"').addClass('text-white');
            $('#app_task').append('<button type="button" class="btn btn-outline-light ms-2" id="goToMenu">Перейти в меню</button>');
            $('#game_extra_circle').removeClass('d-none').fadeIn();
            setTimeout(() => {
                $('#goToMenu').click(() => {
                    showMenu('game_extra_circle', 'background_field_of_shame', game_extra_circle.score);
                });
                setTimeout(() => {
                    // $("#draggable").draggable();
                    let text = `
                    Устав был очень_длинен, и Пьер от_радости,_волнения_и_стыда не_был_в_состоянии_понимать того, что
                читали. Увидав этот страх Наташи, Соня заплакала_слезами стыда и жалости за свою подругу. Он не знал,
                что душа Наташи была преисполнена_отчаяния,_стыда,_унижения, и что она не виновата была в том, что лицо
                ее нечаянно выражало спокойное_достоинство_и_строгость. Вид этого офицера был настолько презрительный и
                высокомерный, что Ростов вдруг почувствовал стыд побежденного и, поспешно_отвернувшись, ушел назад. У
                Иполита это выражение стыда выражалось только в высшей_степени_хохота. Ты не знаешь, что это такое? Это
                погибель нашей армии, стыд. Это измена. Он проснулся и все плакал и плакал_слезами стыда и раскаяния о
                своем падении, навеки_отделившем его от Сони (Л. Н. Толстой «Война и мир»).
                    `;
                    let words = text.trim().split(' ');
                    words.forEach(word => {
                        if (word.includes('_')) {
                            word = word.replaceAll('_', ' ');
                        }
                        $('#draggable_words').append(`<span class="draggable_word">${word} </span>`)
                    });
                    $('#placeholder').hide();
                    $(".draggable_word").draggable({
                        revert: "invalid",
                        containment: "document",
                        helper: "clone",
                        cursor: "move",
                        scroll: true
                    });
                    $("#sortable").sortable({
                        revert: true
                    });
                    $("#droppable").droppable({
                        accept: ".draggable_word",
                        classes: {
                            "ui-droppable-active": "drop-zone",
                            "ui-droppable-hover": "ui-state-hover"
                        },
                        connectToSortable: "#sortable",
                        drop: function (event, ui) {
                            // $(this).find('ul').append(`<li class="list-group-item">${ui.draggable.clone()}}</li>`);
                            
                            $(ui.draggable.clone()).removeClass('draggable_word').
                                appendTo('#droppable ul').wrap('<li class="list-group-item"></li>');
                            $(this).find('.draggable_word').removeClass();
                            // $(this).find('ul').append(`<li class="list-group-item">${cloui.draggablened}</li>`);
                            // $('#droppable').addClass('bg-success');
                        }
                    });

                    $('#game_extra_circle_btn').click(() => {
                        console.log(game_extra_circle.answers);
                        $('#sortable').children().each((index, element) => {
                            let text = $(element).text().trim();
                            console.log(text);
                            if (game_extra_circle.answers.indexOf(text) !== -1) {
                                console.log('match');
                                game_extra_circle.score += 1;
                                $(element).addClass('bg-success');
                            } else {
                                console.log('wrong');
                            }
                            console.log('---');
                        });
                        $('#game_extra_circle_Result').text(game_extra_circle.score);
                        $('#game_extra_circle_Modal').modal('show');
                        console.log(game_extra_circle);
                    });
                }, 1000);
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
                        id="game_millionaire_score"></span></p>
            </div>
        </div>
        <div class="col-6">
            <div class="game text-center position-relative" @click="runGame" data-game="field_of_shame">
                <img src="../public/img/background-3.webp" class="img-fluid rounded " alt="">
                <h3 class="position-absolute top-50 start-0">Определи поле состояния</h3>
                <p>Нажми на картинку чтобы сыграть <span class="alert alert-info  py-0 invisible" role="alert"
                        id="game_field_of_shame_score"></span></p>
            </div>
        </div>
    </div>
    <div class="row list_of_games" style="margin-top: 130px;">
        <div class="col-6">
            <div class="game text-center" @click="runGame" data-game="extra_circle">
                <img src="../public/img/task_3_logo.png" class="img-fluid rounded " alt="">
                <p>Нажми на картинку чтобы сыграть <span class="alert alert-info py-0 invisible" role="alert"
                        id="game_extra_circle_score"></span></p>
            </div>
        </div>
        <div class="col-6">
            <div class="game text-center" @click="runGame" data-game="part_of_speach">
                <img src="../public/img/orig.png" class="img-fluid rounded " alt="">
                <p>Нажми на картинку чтобы сыграть</p>
            </div>
        </div>
    </div>

    <millionaire msg="Vite + Vue" />
    <field_of_shame />
    <extra_circle />
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
