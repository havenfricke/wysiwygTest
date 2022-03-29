<template>
  <header>
    <Navbar />
  </header>
  <main>
    <div id="app">
      <div class="bg-dark text-light p-1 mt-3">
        <button @click="save">save</button>
        <button @click="showPreview = !showPreview">preview</button>
      </div>
      <div v-if="!showPreview">
        <editor
          v-model="editable.bio"
          @selectionChange="saveContent"
          api-key="8cbcxix5kfgyb4dxa8i4jxkjudi7il8b7becshh9yq5218kv"
          :init="{
            height: 500,
            menubar: true,
            plugins: [
              'advlist autolink lists link image charmap print preview anchor',
              'searchreplace visualblocks code fullscreen',
              'insertdatetime media table paste code help wordcount',
            ],
            toolbar:
              'undo redo | formatselect | bold italic backcolor | \
           alignleft aligncenter alignright alignjustify | \
           bullist numlist outdent indent | removeformat | help',
          }"
        />
      </div>
      <div v-else v-html="editable.bio"></div>
    </div>

    <router-view />
  </main>

  <!-- TODO sanitize html on the server before saving it -->
  <footer>
    <div class="bg-dark text-light text-center p-4">
    </div>
  </footer>
</template>

<script>
import { computed, ref } from "vue";
import { AppState } from "./AppState";
import Editor from "@tinymce/tinymce-vue";
export default {
  name: "App",
  components: {
    editor: Editor,
  },

  setup() {
    const editable = ref({
      bio: `
    <h1>This is a heading...</h1>
    this is a test
    
    `,
    });

    const showPreview = ref(false);
    return {
      editable,
      showPreview,
      appState: computed(() => AppState),
      save() {
        console.log(editable.value.bio);
      },
    };
  },
};
</script>
<style lang="scss">
@import "./assets/scss/main.scss";
</style>
