<script setup>
import { ref, onMounted } from 'vue'

const count = ref(0)
</script>

<template>
    <div id="game_field_of_shame" class="container d-none">
        <div class="accordion" id="accordionPanelsStayOpenExample">
            <div class="accordion-item">
                <h2 class="accordion-header" id="panelsStayOpen-headingOne">
                    <button class="accordion-button" type="button" data-bs-toggle="collapse"
                        data-bs-target="#panelsStayOpen-collapseOne" aria-expanded="true"
                        aria-controls="panelsStayOpen-collapseOne">
                        Изучите информационный материал и, используя примеры из художественных текстов, составьте поле
                        состояния стыда в русской культуре
                    </button>
                </h2>
                <div id="panelsStayOpen-collapseOne" class="accordion-collapse collapse show"
                    aria-labelledby="panelsStayOpen-headingOne">
                    <div class="accordion-body">
                        В состав семантического поля входят разноуровневые средства языка (лексические,
                        фразеологические, синтаксические), которые объединены на основе выражаемой ими общей понятийной
                        категории – значения. В поле выделяются ядро и периферия. Компоненты ядра наиболее часто и полно
                        выражают значение поля, периферийные компоненты менее частотны и не так конкретны, их значения
                        варьируются.
                    </div>
                </div>
            </div>
            <div class="accordion-item">
                <h2 class="accordion-header" id="panelsStayOpen-headingTwo">
                    <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse"
                        data-bs-target="#panelsStayOpen-collapseTwo" aria-expanded="false"
                        aria-controls="panelsStayOpen-collapseTwo">
                        Примеры для анализа
                    </button>
                </h2>
                <div id="panelsStayOpen-collapseTwo" class="accordion-collapse collapse"
                    aria-labelledby="panelsStayOpen-headingTwo">
                    <div class="accordion-body">
                        <ol>
                            <li>
                                И нужно было нанимать в дядьки басурмана, как будто у барина не стало и своих людей!
                                “Мне было <strong>стыдно</strong>. Я отвернулся и сказал ему: Поди вон, Савельич; я чаю
                                не
                                хочу (А.С. Пушкин «Капитанская дочка»)
                            </li>
                            <li>
                                <strong>Стыда</strong> и тайной муки полный, Без гнева вытерпев упрек, Ступил опять
                                Гарун безмолвный За
                                неприветливый порог. (М. Ю. Лермонтов «Беглец»)
                            </li>
                            <li>
                                «– Какие глупости вы говорите сегодня! <strong>Стыдитесь</strong>, пожалуйста» (Ф.М.
                                Достоевский «Чужая жена и муж под кроватью»)
                            </li>
                            <li>
                                И ничего – ни утешения и ни горечи – она не ощутила, одно только слабое и далекое
                                удивление да неясный, неизвестно к чему относящийся <strong>стыд</strong> (В. Распутин
                                «Живи и
                                помни»).
                            </li>
                            <li>
                                Они всего боялись и даже перед носильщиками <strong>неловко</strong> и торопливо
                                сдергивали свои растрепанные шапки. (И.А. Бунин «На чужой стороне»)
                            </li>
                            <li>
                                Он это чувствовал, <strong>неловко</strong> улыбался и даже бодрился, а сам думал,
                                сравнивая дочь со старухой: нет, моя душевнее была! (И.А. Бунин «Худая трава»)
                            </li>
                            <li>
                                Священник оробел, <strong>смущенно</strong> ответил, что желал бы совершить служение
                                (И.А. Бунин «Иоанн Рыдалец»).
                            </li>
                            <li>
                                И к чему вообще так настойчиво и неуклонно идет он, изо дня в день опустошая свое
                                разоренное жилье, стремясь дотла искоренить даже следы того, что так случайно было
                                создано диким
                                гением Романа, и непрестанно алкая обиды, <strong>позора</strong> и побоев? (И.А. Бунин
                                «Я все молчу»)
                            </li>
                        </ol>
                    </div>
                </div>
            </div>
        </div>

        <button class="btn btn-success my-2" id="start_movement">
            Начать перетаскивание
        </button>
        <button class="btn btn-danger my-2 ms-3" id="end_movement">
            Завершить перетаскивание
        </button>
        <div class="row" id="drag_container">
            <div class="col game_field_of_shame_drop border-end border-danger" id="game_field_of_shame_drop">
                <p>Перетащите объекты из правой части в левую, чтобы построить поле состояния стыда.</p>
                <p>Нажмите на кнопку <strong>"Начать перетаскивание"</strong> для начала игры</p>
                <p>Нажмите на кнопку <strong>"Завершить перетаскивание"</strong> чтобы перейти к следующему этапу.</p>
            </div>
            <div class="col game_field_of_shame_drag">
                <div class="border-bottom border-danger" id="figure-initial-place">
                    <img src="../../public/img/core_circle.png" alt="" id="core_circle">
                    <img src="../../public/img/external_circle.png" alt="" id="external_circle">
                    <div class="empty"></div>
                </div>
                <div>
                    <h3><span class="badge text-bg-primary">Ядро</span></h3>
                    <input type="text" class="form-control" id="core_cicle_input"
                        placeholder="Введите слова через запятую">
                    <h3><span class="badge text-bg-danger mt-4">Переферия</span></h3>
                    <input type="text" class="form-control" id="external_cicle_input"
                        placeholder="Введите слова через запятую">
                    <button type="button" class="btn btn-primary mt-3 invisible"
                        id="game_field_of_shame_check">Выполнить</button>
                </div>
            </div>
        </div>
        <div class="toast-container bottom-0 end-0">
            <div class="toast" role="alert" aria-live="assertive" aria-atomic="true" id="toast" data-autohide="true"
                data-bs-delay="3000">
                <div class=" toast-header">
                    <i class="bi bi-bell-fill text-success fs-3"></i>
                    <strong class="me-auto">Уведомление</strong>
                    <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="Close"></button>
                </div>
                <div class="toast-body">
                    Вы можете начать перетаскивание.
                </div>
            </div>
        </div>

    </div>


</template>