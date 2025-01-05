<template>
    <div class="main-editor" :class="{ 'expanded': isExpanded }">
        
    </div>
</template>

<script>
/* global diff_match_patch */
import _ from 'cledit';
import '@/components/Editor/mdGrammar.js';
import Prism from 'prismjs';

export default {
    mounted() {
        const editor = window.cledit(document.querySelector('.main-editor'));
        editor.init({
            sectionHighlighter: function (section) {
                return Prism.highlight(section.text, 
                    window.mdGrammar({
                        fences: true,
                        tables: true,
                        footnotes: true,
                        abbrs: true,
                        deflists: true,
                        tocs: true,
                        dels: true,
                        subs: true,
                        sups: true
                    })
                );
            },
            // sectionParser: function (text) {
            //     let offset = 0;
            //     let sectionList = [];
            //     ;(text + '\n\n').replace(/^.+[ \t]*\n=+[ \t]*\n+|^.+[ \t]*\n-+[ \t]*\n+|^\#{1,6}[ \t]*.+?[ \t]*\#*\n+/gm, function (match, matchOffset) {
            //         sectionList.push(text.substring(offset, matchOffset))
            //         offset = matchOffset
            //     });
            //     sectionList.push(text.substring(offset));
            //     return sectionList;
            // }
        })
    },
    name: 'TextEditor',
    props: {
        isExpanded: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            content: '',
            lastAstrisk: -1,
        }
    },
    methods: {
        
        handleInput(event) {
            this.content = this.$refs.editableDiv.innerHTML;
            
            this.$emit('content-change', this.content);

        }
    },
    watch: {
        content(newContent) {
            if (this.$refs.editableDiv.innerHTML !== newContent) {
                this.$refs.editableDiv.innerHTML = newContent;
            }
        }
    }
}
</script>

<style scoped>
.main-editor {
    flex: 1;
    background-color: var(--color-background);
    transition: margin-left 0.3s ease;
    padding: 20px;
}

.main-editor.expanded {
    margin-left: -210px;
}

.editor-content {
    width: 100%;
    height: 100%;
    min-height: 100%;
    color: var(--color-text);
    font-size: 1rem;
    line-height: 1.5;
    outline: none;
    white-space: pre-wrap;
    overflow-y: auto;
}

.editor-content:empty:before {
    content: 'Start typing...';
    color: var(--color-text-lighter);
}
</style>
