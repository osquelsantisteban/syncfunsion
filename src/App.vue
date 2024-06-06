<template>
  <RichTextEditorComponent ref="rteInstance" height="200px" width="700px" :toolbarSettings="toolbarSettings">
    <img src="https://ej2.syncfusion.com/demos/src/rich-text-editor/images/RTEImage-Feather.png"
         alt="Logo" style="height:150px; width:150px;">
    <p>
      <a href="https://ej2.syncfusion.com/vue/documentation/rich-text-editor/link">Rich Text Editor</a> 
      component is a WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content. Users can format their content using standard toolbar commands.
    </p>
  </RichTextEditorComponent>
</template>

<script setup>
import { ref, defineComponent, provide } from 'vue';
import { RichTextEditorComponent, Toolbar, Image, HtmlEditor, Link, Table, QuickToolbar } from '@syncfusion/ej2-vue-richtexteditor';

// Usar ref para crear una referencia al componente del editor
const rteInstance = ref(null);

// Configuración de la barra de herramientas
const toolbarSettings = ref({
  items: ['Bold', 'Italic', 'Undo', 'Redo', 'CreateTable', 'Image', 'CreateLink']
});

// Método para manejar el clic, adaptado para Composition API
function click() {
  if (rteInstance.value) {
    const content = rteInstance.value.getHtml();
    console.log(content);
  }
}

// Proveer dependencias de Syncfusion necesarias para el componente
provide('richtexteditor', [Toolbar, Image, HtmlEditor, Link, Table, QuickToolbar]);
</script>

<style>
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-lists/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-vue-richtexteditor/styles/material.css";
</style>