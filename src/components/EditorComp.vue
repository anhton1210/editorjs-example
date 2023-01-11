<template>
  <div id="app">
    <div id="editorjs"></div>
    <div class="ce-example__statusbar">
      <div class="ce-example__statusbar-item">
        Readonly:
        <b id="readonly-state">
          Off
        </b>
        &nbsp;
        <div class="ce-example__statusbar-button" @click="toggleReadOnly">
          toggle
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import EditorJS from "@editorjs/editorjs";
import Header from "@editorjs/header";
import Paragraph from "@editorjs/paragraph";
import NestedList from "@editorjs/nested-list";
import Marker from "@editorjs/marker";
import SimpleImage from "@editorjs/simple-image";
import Quote from "@editorjs/quote";
import Checklist from "@editorjs/checklist";
import CodeTool from "@editorjs/code";
import Delimiter from "@editorjs/delimiter";
import Embed from "@editorjs/embed";
import RawTool from "@editorjs/raw";
import Table from "@editorjs/table";
import LinkTool from "@editorjs/link";
import InlineCode from "@editorjs/inline-code";
import Underline from '@editorjs/underline';

export default {
  name: "EditorComp",
  data() {
    return {
      value: null,
      editorConfig: {
        /**
         * Enable/Disable the read only mode
         */
        readOnly: false,

        /**
         * Wrapper of Editor
         */
        holder: 'editorjs',
        // inlineToolbar: ['link', 'marker', 'bold', 'italic', 'underline'],
        inlineToolbar: true,

        /**
         * Tools list
         */
        tools: {
          header: {
            class: Header,
            inlineToolbar: ['marker', 'link'],
            config: {
              placeholder: 'Header'
            },
          },

          image: SimpleImage,

          underline: Underline,

          list: {
            class: NestedList,
            inlineToolbar: true,
          },
          paragraph: {
            class: Paragraph,
            config: {
              placeholder: "."
            }
          },

          checklist: {
            class: Checklist,
            inlineToolbar: true,
          },

          quote: {
            class: Quote,
            inlineToolbar: true,
            config: {
              quotePlaceholder: 'Enter a quote',
              captionPlaceholder: 'Quote\'s author',
            },
          },

          marker: {
            class:  Marker,
          },

          code: {
            class:  CodeTool,
          },

          delimiter: Delimiter,

          inlineCode: {
            class: InlineCode,
          },

          linkTool: LinkTool,

          raw: RawTool,

          embed: Embed,

          table: {
            class: Table,
            inlineToolbar: true,
          },
        },

        /**
         * This Tool will be used as default
         */
        // defaultBlock: 'paragraph',

        /**
         * Initial Editor data
         */
        data: {
          blocks: [
            {
              id: "zcKCF1S7X8",
              type: "header",
              data: {
                text: "Editor.js",
                level: 1
              }
            },
            {
              "id": "b6ji-DvaKb",
              "type": "paragraph",
              "data": {
                "text": "Hey. Meet the new Editor. On this page you can see it in action — try to edit this text. Source code of the page contains the example of connection and configuration."
              }
            },
            {
              type: "header",
              id: "7ItVl5biRo",
              data: {
                text: "Key features",
                level: 2
              }
            },
            {
              type : 'list',
              id: "SSBSguGvP7",
              data : {
                items : [
                  {
                    content: 'It is a block-styled editor',
                    items: []
                  },
                  {
                    content: 'It returns clean data output in JSON',
                    items: []
                  },
                  {
                    content: 'Designed to be extendable and pluggable with a simple API',
                    items: []
                  }
                ],
                style: 'unordered'
              }
            },
            {
              type: "header",
              id: "QZFox1m_ul",
              data: {
                text: "What does it mean «block-styled editor»",
                level: 2
              }
            },
            {
              type : 'paragraph',
              id: "mTrPOHAQTe",
              data : {
                text : `There are dozens of <a href="https://github.com/editor-js">ready-to-use Blocks</a> and the <a href="https://editorjs.io/creating-a-block-tool">simple API</a> for creation any Block you need. For example, you can implement Blocks for Tweets, Instagram posts, surveys and polls, CTA-buttons and even games.`
              }
            },
            {
              type: "header",
              id: "1sYMhUrznu",
              data: {
                text: "What does it mean clean data output",
                level: 2
              }
            },
            {
              type : 'paragraph',
              id: "0lOGNUKxqt",
              data : {
                text : `Given data can be used as you want: render with HTML for <code class="inline-code">Web clients</code>, render natively for <code class="inline-code">mobile apps</code>, create markup for <code class="inline-code">Facebook Instant Articles</code> or <code class="inline-code">Google AMP</code>, generate an <code class="inline-code">audio version</code> and so on.`
              }
            },
            {
              type : 'paragraph',
              id: "WvX7kBjp0I",
              data : {
                text : 'Clean data is useful to sanitize, validate and process on the backend.'
              }
            },
            {
              type : 'delimiter',
              id: "H9LWKQ3NYd",
              data : {}
            },
            {
              type: 'image',
              id: "9802bjaAA2",
              data: {
                url: 'https://cdn.georgiatechbootcamp.com/wp-content/uploads/sites/95/2021/08/tes_gen_blog_post_071921_1233182206-800x412.jpg',
                // caption: '',
                stretched: false,
                withBorder: true,
                withBackground: false,
              }
            },
          ]
        },
        onReady: function(){
          console.log('Editor.js is ready to work!')
        },
        onChange: function(api, event) {
          console.log('something changed', event);
        },
      },
    };
  },
  methods: {
    myEditor() {
      this.editor = new EditorJS(this.editorConfig);
      this.editor.isReady
      .then(() => {
        console.log("Editor.js·is·ready·to·work!");
      })
      .catch((reason) => {
        console.log(`Editor.js·initialization·failed·because·of·${reason}`);
      });
    },
    async toggleReadOnly() {
      const readOnlyState = await this.editor.readOnly.toggle();
      const readOnlyIndicator = document.getElementById('readonly-state');

      readOnlyIndicator.textContent = readOnlyState ? 'On' : 'Off';
    }
  },
  created() {
    this.myEditor();
  },
};
</script>

<style scoped>
.ce-example__statusbar {
  display: flex;
  align-items: center;
  position: fixed;
  bottom: 0;
  right: 0;
  left: 0;
  background: #fff;
  border-radius: 8px 8px 0 0;
  border-top: 1px solid #E8E8EB;
  box-shadow: 0 2px 6px #E8E8EB;
  font-size: 13px;
  padding: 8px 15px;
  z-index: 1;
  user-select: none;
}

@media (max-width: 768px) {
  .ce-example__statusbar {
    display: none;
  }
}

.ce-example__statusbar-item:not(:last-of-type)::after {
  content: '|';
  color: #ddd;
  margin: 0 15px 0 12px;
}

.ce-example__statusbar-item--right {
  margin-left: auto;
}

.ce-example__statusbar-button {
  display: inline-block;
  padding: 3px 12px;
  transition: all 150ms ease;
  cursor: pointer;
  border-radius: 31px;
  background: #eff1f4;
  text-align: center;
  user-select: none;
}

.ce-example__statusbar-button:hover {
  background: #e0e4eb;
}

.ce-example__statusbar-button-primary {
  background: #4A9DF8;
  color: #fff;
  box-shadow: 0 7px 8px -4px rgba(137, 207, 255, 0.77);
  font-family: 'PT Mono', Menlo, Monaco, Consolas, Courier New, monospace;
}

.ce-example__statusbar {
  --toggler-size: 20px;
}

.ce-example__statusbar-toggler {
  position: relative;
  background: #7b8799;
  border-radius: 20px;
  padding: 2px;
  width: calc(var(--toggler-size) * 2.2);
  cursor: pointer;
  user-select: none;
}

.ce-example__statusbar-toggler::before {
  display: block;
  content: '';
  width: var(--toggler-size);
  height: var(--toggler-size);
  background: #fff;
  border-radius: 50%;
  transition: transform 100ms ease-in;
}

.ce-example__statusbar-toggler::after {
  --moon-size: calc(var(--toggler-size) * 0.5);
  content: '';
  position: absolute;
  top: 5px;
  right: 5px;
  height: var(--moon-size);
  width: var(--moon-size);
  box-shadow: calc(var(--moon-size) * 0.25 * -1) calc(var(--moon-size) * 0.18) 0 calc(var(--moon-size) * 0.05) white;
  border-radius: 50%;
}
</style>
