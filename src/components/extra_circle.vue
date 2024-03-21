<script setup>
import { ref, onMounted } from 'vue'

defineProps({
    msg: String,
})

const count = ref(0)
</script>

<template>
    <div id="game_extra_circle" class="container d-none">
        <div class="alert alert-success" role="alert">
            <h4 class="alert-heading">
                Смоделируйте периферию семантического поля стыд, составляя ассоциативное поле к понятию «стыд» на основе
                приведенных примеров из романа Л.Н. Толстого «Война и мир»:
            </h4>
            <p id="draggable_words">
                <span class="placeholder col-12 bg-success" id="placeholder"></span>
            </p>
            <hr>
            <p class="mb-0">
            <div class="row">
                <div class="col-4">
                    <img src="../../public/img/task_3.png" alt="" id="core_circle">
                </div>
                <div class="col-8 droppable" id="droppable">
                    <ul class="list-group" id="sortable">
                    </ul>
                </div>
            </div>
            </p>
        </div>
        <div class="float-end">
            <button type="button" class="btn btn-success" id="game_extra_circle_btn">Проверить</button>
        </div>
        <!-- Modal -->
        <div class="modal fade" id="game_extra_circle_Modal" tabindex="-1" aria-labelledby="exampleModalLabel"
            aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">Результат</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        Вы набрали <span id="game_extra_circle_Result" class="text-primary"></span> баллов из 12.
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Закрыть</button>
                    </div>
                </div>
            </div>
        </div>
    </div>


</template>
