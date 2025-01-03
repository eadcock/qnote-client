<template>
    <div class="side-panel" :class="{ 'collapsed': isPanelCollapsed }">
        <button class="collapse-btn" @click="togglePanel">
            {{ isPanelCollapsed ? '›' : '‹' }}
        </button>
        <div class="panel-content" v-show="!isPanelCollapsed">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SidePanel',
    data() {
        return {
            isPanelCollapsed: false
        }
    },
    methods: {
        togglePanel() {
            this.isPanelCollapsed = !this.isPanelCollapsed;
            this.$emit('panel-toggle', this.isPanelCollapsed);
        }
    }
}
</script>

<style scoped>
.side-panel {
    width: 250px;
    background-color: var(--vt-c-background-lighter);
    position: relative;
    transition: width 0.3s ease;
}

.side-panel.collapsed {
    width: 40px;
}

.collapse-btn {
    position: absolute;
    right: -1px;
    top: 20px;
    z-index: 1;
    border: 1px solid #ddd;
    background: white;
    padding: 8px;
    cursor: pointer;
    border-radius: 4px;
}

.panel-content {
    padding: 20px;
}
</style>
