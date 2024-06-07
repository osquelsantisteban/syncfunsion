<template>
  <button class="e-btn e-primary" @click="handleSave">Save</button>

  <RichTextEditorComponent 
    height="400px" 
    width="1000px" 
    ref="rteInstance" 
    :toolbarSettings="customtoolbarSettings"
    :floatingToolbarOffset="50"
    :quickToolbarSettings="customtoolbarSettings.quickToolbarSettings"
    >
    <img src="https://ej2.syncfusion.com/demos/src/rich-text-editor/images/RTEImage-Feather.png"
         alt="Logo" style="height:150px; width:150px;">
    <p>
      <a href="https://ej2.syncfusion.com/vue/documentation/rich-text-editor/link">Rich Text Editor</a> 
      component is a WYSIWYG editor that provides the best user experience to create and update the content. Users can format their content using standard toolbar commands.
    </p>
  </RichTextEditorComponent>

  <DialogComponent 
    width="30%" 
    ref="dialogObj"
    :header="dialogSettings.header"
    :showCloseIcon="dialogSettings.showCloseIcon"
    :visible="dialogSettings.visible"
    :isModal="dialogSettings.modal"
    :content="'contentTemplate'"
  >
  <template v-slot:contentTemplate>
          <div id="customTbarDialog" >
          <div id="rteSpecial_char">
            <div class="char_block" title="&#94;">&#94;</div>
            <div class="char_block" title="&#95;">&#95;</div>
            <div class="char_block" title="&#96;">&#96;</div>
            <div class="char_block" title="&#123;">&#123;</div>
            <div class="char_block" title="&#124;">&#124;</div>
            <div class="char_block" title="&#125;">&#125;</div>
            <div class="char_block" title="&#126;">&#126;</div>
            <div class="char_block" title="&#160;">&#160;</div>
            <div class="char_block" title="&#161;">&#161;</div>
            <div class="char_block" title="&#162;">&#162;</div>
            <div class="char_block" title="&#163;">&#163;</div>
            <div class="char_block" title="&#164;">&#164;</div>
            <div class="char_block" title="&#165;">&#165;</div>
            <div class="char_block" title="&#x20B9;">&#x20B9;</div>
            <div class="char_block" title="&#166;">&#166;</div>
            <div class="char_block" title="&#167;">&#167;</div>
            <div class="char_block" title="&#168;">&#168;</div>
            <div class="char_block" title="&#169;">&#169;</div>
            <div class="char_block" title="&#170;">&#170;</div>
            <div class="char_block" title="&#171;">&#171;</div>
            <div class="char_block" title="&#172;">&#45;</div>
            <div class="char_block" title="&#173;">&#173;</div>
            <div class="char_block" title="&#174;">&#174;</div>
            <div class="char_block" title="&#175;">&#175;</div>
            <div class="char_block" title="&#176;">&#176;</div>
            <div class="char_block" title="&#177;">&#177;</div>
            <div class="char_block" title="&#178;">&#178;</div>
            <div class="char_block" title="&#179;">&#179;</div>
            <div class="char_block" title="&#180;">&#180;</div>
            <div class="char_block" title="&#181;">&#181;</div>
            <div class="char_block" title="&#182;">&#182;</div>
            <div class="char_block" title="&#183;">&#183;</div>
            <div class="char_block" title="&#184;">&#184;</div>
            <div class="char_block" title="&#185;">&#185;</div>
            <div class="char_block" title="&#186;">&#186;</div>
            <div class="char_block" title="&#187;">&#187;</div>
            <div class="char_block" title="&#188;">&#188;</div>
            <div class="char_block" title="&#189;">&#189;</div>
            <div class="char_block" title="&#190;">&#190;</div>
            <div class="char_block" title="&#191;">&#191;</div>
            <div class="char_block" title="&#192;">&#192;</div>
            <div class="char_block" title="&#193;">&#193;</div>
            <div class="char_block" title="&#194;">&#194;</div>
            <div class="char_block" title="&#195;">&#195;</div>
          </div>
    </div>
  </template>
  </DialogComponent>

</template>

<script setup>
import { ref, reactive, provide } from 'vue';
import { RichTextEditorComponent, Toolbar, Image, HtmlEditor, Link, Table, QuickToolbar } from '@syncfusion/ej2-vue-richtexteditor';
import { DialogComponent } from "@syncfusion/ej2-vue-popups";

const rteInstance = ref(null);
const dialogObj = ref(null);

// Reactive state for dialog settings
const dialogSettings = reactive({
  header: "Select the Special Character",
  showCloseIcon: true,
  visible: false,
  modal: true,
});

const customModalSymbol = () => {
  if (rteInstance.value && dialogObj.value) {
    // Enfoca el panel de edición.
    const editor = rteInstance.value.ej2Instances.contentModule.getEditPanel();
    editor.focus();

    const range = rteInstance.value.ej2Instances.selection.getRange(document);
    const savedSelection = rteInstance.value.ej2Instances.selection.save(range, document);
    
    // Guarda la selección en alguna propiedad reactiva si necesitas acceder a ella más tarde.
    rteInstance.value.savedSelection = savedSelection;

    // Muestra el diálogo
    dialogSettings.visible = true;
  }
};

const customtoolbarSettings = {
  items: [
    'Bold', 'Italic', 'Underline', 'StrikeThrough',
    'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
    'LowerCase', 'UpperCase', '|',
    'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
    'Outdent', 'Indent', '|', 'CreateTable',
    'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
    'SourceCode', 'FullScreen', '|', 'Undo', 'Redo',
    {
      template: '<button id="custom_tool" class="e-tbar-btn e-control e-btn e-lib e-icon-btn">' +
                '<span class="e-tbar-btn-text">&#937;</span></button>',
      tooltipText: "Insert Symbol",
      click: customModalSymbol
    }
  ],
  type: 'MultiRow',
  quickToolbarSettings: {
    image: ['Replace', 'Align', 'Caption', 'Remove', 'InsertLink', 'OpenImageLink', '|', 
            'EditImageLink', 'RemoveImageLink', 'Display', 'AltText', 'Dimension']
  }
};


const handleSave = () => {
  if (rteInstance.value) {
    const content = rteInstance.value.getHtml();
    console.log(content);
  }
};

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
  #rteSpecial_char .char_block {
  display: inline-block;
}

#rteSpecial_char {
  padding: 15px 0 15px 0;
}

#rteSpecial_char .char_block.e-active {
  outline: 1px solid #e3165b;
  border-color: #e3165b;
}

#rteSpecial_char .char_block {
  width: 30px;
  height: 30px;
  line-height: 30px;
  margin: 0 5px 5px 0;
  text-align: center;
  vertical-align: middle;
  border: 1px solid #dddddd;
  font-size: 20px;
  cursor: pointer;
  user-select: none;
}
</style>