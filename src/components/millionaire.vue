<script setup>
import { ref, onMounted } from 'vue'

defineProps({
    msg: String,
})

const count = ref(0)
</script>

<template>
    <div id="game_millionaire" class="container">
        <div class="card border-primary mb-3">
            <div class="card-header">Задание 1</div>
            <div class="card-body text-primary">
                <h4  class="card-title">Проанализируйте средства выражения семантики стыда в приведенных примерах из
                    художественных произведений.</h4>
                <p class="fst-italic">
                    И нужно было нанимать в дядьки басурмана, как будто у барина не стало и своих л юдей! “ Мне было
                    стыдно. Я отвернулся и сказал ему: Поди вон, Савельич; я чаю не хочу (А.С. Пушкин «Капитанская
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
            </div>
        </div>
    </div>


</template>
