<template>
    <div class="simditor">
        <textarea :id="id"></textarea>
    </div>
</template>
<script>
    import $ from 'jquery'
    import Simditor from 'simditor'
    import 'simditor/styles/simditor.css'

    export default {
        name: 'simditor',
        data() {
            return {
                editor: '',
                options: {}
            }
        },
        props: {
            id: {
                default() {
                    return 'editor'
                }
            },  //这里传入动态id，一个页面能使用多个编辑器
        },
        mounted() {
            let vm = this;
            this.editor = new Simditor(Object.assign({}, {
                textarea: $(`#${vm.id}`)
            }, this.options));
            this.editor.on('valuechanged', (e, src) => {
                this.valueChange(e, src)
            })
        },
        methods: {
            valueChange() {
                this.$emit('change', this.editor.getValue())
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>