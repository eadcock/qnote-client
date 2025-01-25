<template>
    <div class="main-editor" :class="{ 'expanded': isExpanded }"></div>
</template>

<script>
import dmp from 'googlediff';
window.diff_match_patch = dmp;
// aight, fuck cledit
// import '@/../node_modules/cledit/dist/cledit.js';
// import '@/components/Editor/mdGrammar.js';
import {schema} from "prosemirror-markdown"
import {EditorState} from "prosemirror-state"
import {EditorView} from "prosemirror-view"
import {undo, redo, history} from "prosemirror-history"
import {keymap} from "prosemirror-keymap"

export default {
    mounted() {
      const editor = document.querySelector('.main-editor');
      let state = EditorState.create({
        schema,
        plugins: [
          history(),
          keymap({"Mod-z": undo, "Mod-y": redo})
        ]
      });
      let view = new EditorView(editor, {
        state,
        dispatchTransaction(trans) {
            console.log("Document size went from", trans.before.content.size,
              "to", trans.doc.content.size);
            let newState = view.state.apply(trans);
            view.updateState(newState);
        }
      });

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
            console.log(this.content);
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

<style src="prismjs/themes/prism-dark.css"></style>
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
