<template>
    <div>
        <button @click="getData">get Data</button>
        <div ref="content" id="content"></div>
    </div>
</template>

<script>

    import ClassicEditor from '@ckeditor/ckeditor5-build-classic'

    export default {
        name: "ckEditor",
        mounted() {
            ClassicEditor.builtinPlugins.map(plugin => console.log(plugin.pluginName));
            /*  所有插件:
            *   Essentials
                CKFinderUploadAdapter
                Autoformat
                Bold
                Italic
                BlockQuote
                CKFinder
                EasyImage
                Heading
                Image
                ImageCaption
                ImageStyle
                ImageToolbar
                ImageUpload
                Indent
                Link
                List
                MediaEmbed
                Paragraph
                PasteFromOffice
                Table
                TableToolbar
                TextTransformation
            * */
            ClassicEditor.create(this.$refs.content, {
                // 工具栏的配置, |为分割线
                toolbar: ['heading', '|', 'bold', '|', 'italic', 'bulletedList', 'numberedList', 'blockQuote'],
                heading: {
                    options: [
                        {model: 'paragraph', title: '默认', class: 'ck-heading_paragraph'},
                        {model: 'heading1', view: 'h1', title: '标题 1', class: 'color-red'}
                    ]
                }
            })
                .then(editor => {
                    this.editor = editor;

                    // 设置默认值方法
                    this.editor.setData('<p style="color: #fafafa;"> default Data </p>')

                    // 销毁方法
                    setTimeout(() => {
                        this.editor.destroy()
                            .catch(error => {
                                console.log('销毁失败');
                            })
                    }, 1000 * 60 * 60 * 24 * 365);

                    // // 设置监听方法
                    // this.editor.model.document.on('change:data', (e) => {
                    //     console.log('data change', e);
                    // })
                })
                .catch(error => {
                    console.warning(error);
                });

        },
        data() {
            return {
                editor: {}
            }
        },
        methods: {
            getData() {
                console.log(
                    this.editor.getData());
            }
        }
    }
</script>

<style scoped lang="scss">
    /deep/ .color-red {
        color: red;
    }
</style>