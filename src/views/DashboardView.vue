<template>
    <main class="dashboard">
        <SidePanel @panel-toggle="handlePanelToggle">
            Side Panel Content
        </SidePanel>
        <Editor 
            :isExpanded="isPanelCollapsed"
            @content-change="handleContentChange"
        />
    </main>
</template>

<script>
import SidePanel from '@/components/SidePanel.vue'
import Editor from '@/components/Editor/Editor.vue'

export default {
    name: 'DashboardView',
    components: {
        SidePanel,
        Editor
    },
    data() {
        return {
            isPanelCollapsed: false
        }
    },
    methods: {
        handlePanelToggle(isCollapsed) {
            this.isPanelCollapsed = isCollapsed;
        },
        handleContentChange(content) {
            // Handle content changes here
            console.log('Content updated:', content);
        }
    }
}
</script>

<style scoped>
.dashboard {
    display: flex;
    height: 100%;
    width: 100%;
}
</style>