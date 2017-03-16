<template>

    <div class="main">
        <h2>Practice!</h2>

        <ul>
            <li v-for="(section, index) in session" :key="section.id">
                <h3>{{ section }}</h3>
                <button @click="session.splice(index, 1)">X</button>
            </li>
        </ul>

        <section class="add">
            <h3>Add...</h3>

            <select v-model="current.task">
                <option v-for="task in tasks">{{ task }}</option>
            </select>

            <ul v-if="current.task && current.task.length">

                <li>...for <input type="number" min="1" v-model="current.time"> minute{{ current.time > 1 ? 's' : '' }}</li>

                <li v-if="current.task == 'metronome'">...with measures:
                    <ul>
                        <li v-for="(measure, index) in current.pattern">
                            <input type="number" min="1" v-model="measure.beats"> beat{{ measure.beats > 1 ? 's' : '' }} at <input type="number" min="1" v-model="measure.bpm"> bpm <button @click="current.pattern.splice(index, 1)">X</button>
                        </li>
                        <li>
                            <button @click="current.pattern.push({ beats: 4, bpm: 90 })">+</button>
                        </li>
                    </ul>
                </li>

                <button @click="addCurrent">Add!</button>

            </ul>

        </section>

    </div>

</template>

<script>

    export default {
        data(){
            return {
                tasks: [
                    'timer',
                    'metronome'
                ],
                current: {
                    task: '',
                    time: 1,
                    pattern: []
                },
                session: []
            }
        },
        methods: {
            addCurrent: function(){
                this.current.id = Date.now()
                this.session.push( this.current )
                this.current = {
                    task: '',
                    time: 1,
                    pattern: []
                }
            }
        }
    }

</script>
