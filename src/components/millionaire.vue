<script setup>
import { ref, onMounted } from 'vue'

defineProps({
    msg: String,
})

const count = ref(0)
</script>

<template>
    <div id="game_millionaire" class="container d-none">
        <div class="card border-primary mb-3" id="game_millionaire_q1">
            <div class="card-header">Задание 1</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u></h4>
                <p class="fst-italic">
                    И нужно было нанимать в дядьки басурмана, как будто у барина не стало и своих л юдей! “Мне было
                    <strong>стыдно</strong>. Я отвернулся и сказал ему: Поди вон, Савельич; я чаю не хочу (А.С. Пушкин
                    «Капитанская
                    дочка»)
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>
        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q2">
            <div class="card-header">Задание 2</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u></h4>
                <p class="fst-italic">
                    «– Какие глупости вы говорите сегодня! <strong>Стыдитесь</strong>, пожалуйста» (Ф.М. Достоевский
                    «Чужая жена и муж
                    под кроватью»)
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>
        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q3">
            <div class="card-header">Задание 3</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u></h4>
                <p class="fst-italic">
                    И ничего – ни утешения и ни горечи – она не ощутила, одно только слабое и далекое удивление да
                    неясный, неизвестно к чему относящийся <strong>стыд</strong> (В. Распутин «Живи и помни»).
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>

        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q4">
            <div class="card-header">Задание 4</div>
            <div class="card-body text-primary">
                <h4 class="card-title">
                    Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u>
                </h4>
                <p class="fst-italic">
                    Они всего боялись и даже перед носильщиками <strong>неловко</strong> и торопливо сдергивали свои
                    растрепанные шапки.
                    (И.А. Бунин «На чужой стороне»)
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>

        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q5">
            <div class="card-header">Задание 5</div>
            <div class="card-body text-primary">
                <h4 class="card-title">
                    Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u>
                </h4>
                <p class="fst-italic">
                    Он это чувствовал, <strong>неловко</strong> улыбался и даже бодрился, а сам думал, сравнивая дочь со
                    старухой: нет,
                    моя душевнее была! (И.А. Бунин «Худая трава»)
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>

        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q6">
            <div class="card-header">Задание 6</div>
            <div class="card-body text-primary">
                <h4 class="card-title">
                    Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u>
                </h4>
                <p class="fst-italic">
                    Священник оробел, <strong>смущенно</strong> ответил, что желал бы совершить служение (И.А. Бунин
                    «Иоанн Рыдалец»).
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>

        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q7">
            <div class="card-header">Задание 7</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u></h4>
                <p class="fst-italic">
                    И к чему вообще так настойчиво и неуклонно идет он, изо дня в день опустошая свое разоренное жилье,
                    стремясь дотла искоренить даже следы того, что так случайно было создано диким гением Романа, и
                    непрестанно алкая обиды, <strong>позора</strong> и побоев? (И.А. Бунин «Я все молчу»)
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>

        </div>
        <div class="card border-primary mb-3 d-none" id="game_millionaire_q8">
            <div class="card-header">Задание 8</div>
            <div class="card-body text-primary">
                <h4 class="card-title">Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений. <u>Возможны несколько вариантов.</u></h4>
                <p class="fst-italic">
                    <strong>Стыда</strong> и тайной муки полный, Без гнева вытерпев упрек, Ступил опять Гарун безмолвный
                    За неприветливый
                    порог. (М. Ю. Лермонтов «Беглец»)
                </p>
                <div class="row button-section mt-5">
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            A. проективный (соматический) способ
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            C. указания на последствия, к которым состояние стыда может привести
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            E. отражение стыда через описание качеств, которых стыдится или стесняется человек
                        </button>
                    </div>
                    <div class="col-3 text-center">
                        <button type="button" class="btn btn-outline-dark">
                            G. описание отношения к себе и окружающим людям человека, совершившего постыдный поступок
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            B. сопоставление испытываемых человеком чувств с состоянием окружающей среды
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            D. отсылка слушателя (читателя) к общеизвестным, стереотипным ситуациям
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            F. «парадоксальный» способ отражения состояния стыда
                        </button>
                    </div>
                    <div class="col-3 text-center mt-2">
                        <button type="button" class="btn btn-outline-dark">
                            H. использование средств словесной выразительности, в частности - метафор
                        </button>
                    </div>
                </div>
                <div class="float-end mt-3">
                    <button class="btn btn-warning game_millionaire_next me-5 invisible">Далее</button>
                    <button class="btn btn-primary game_millionaire_answer">Ответить</button>
                </div>
            </div>
        </div>
        <div class="card border-success mb-3 d-none" id="game_millionaire_q9">
            <div class="card-header">Итоги</div>
            <div class="card-body text-success">
                <h4 class="card-title">
                    Вы набрали <strong id="game_millionaire_score"></strong> балла из 10.
                </h4>
            </div>
        </div>
    </div>


</template>
