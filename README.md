# vue-codemirror6

A component for using [CodeMirror6](https://codemirror.net/6/) with Vue. Unlike [surmon-china's vue-codemirror](https://github.com/surmon-china/vue-codemirror), it is for CodeMirror6.

## Usage

This component can handle bidirectional binding by `v-model` like a general Vue component.

Other options are currently as follows:

| attribute  | information                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- |
| lang       | The language you want to have syntax highlighting. see <https://codemirror.net/6/#languages>                                     |
| phrases    | Specify here if you want to make the displayed character string multilingual. see <https://codemirror.net/6/examples/translate/> |
| extensions | Includes enhancements to extend CodeMirror. Such as [@codemirror/basic-setup](https://github.com/codemirror/basic-setup).        |
| dark       | Toggle Darkmode.                                                                                                                 |
| linter     | Set Linter. see example <https://codesandbox.io/s/f6nb0?file=/src/index.js>                                                      |

## Example

When using as a Markdown editor on [Vuetify](https://vuetifyjs.com/).

```vue
<template>
  <codemirror
    v-model="value"
    :lang="lang"
    :phrases="phreses"
    :extensions="extensions"
    :dark="$vuetify.theme.dark"
    @update="onCmUpdate"
  />
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

// Load component
import CodeMirror from 'vue-codemirror6';

// CodeMirror extensions
import { basicSetup } from '@codemirror/basic-setup';
import { markdown } from '@codemirror/lang-markdown';
import type { ViewUpdate } from '@codemirror/view';
import type { Extension } from '@codemirror/state';
import type { LanguageSupport } from '@codemirror/language';

@Component({ components: { CodeMirror } })
export default class Home extends Vue {
  /** text */
  value: string;

  /**
   * CodeMirror Language
   *
   * @see {@link https://codemirror.net/6/docs/ref/#language | @codemirror/language}
   */
  lang: LanguageSupport = markdown();

  /**
   * Internationalization Config. In this example, the display language is Japanese.
   *
   * @see {@link https://codemirror.net/6/examples/translate/ | Example: Internationalization}
   */
  phrases: Record<string, string> = {
    // @codemirror/view
    'Control character': '制御文字',
    // @codemirror/fold
    'Folded lines': '折り畳まれた行',
    'Unfolded lines': '折り畳める行',
    to: '行き先',
    'folded code': '折り畳まれたコード',
    unfold: '折り畳む解除',
    'Fold line': '行を折り畳む',
    'Unfold line': '行の折り畳む解除',
    // @codemirror/search
    'Go to line': '行き先の行',
    go: 'OK',
    Find: '検索',
    Replace: '置き換え',
    next: '▼',
    previous: '▲',
    all: 'すべて',
    'match case': '一致条件',
    regexp: '正規表現',
    replace: '置き換え',
    'replace all': 'すべてを置き換え',
    close: '閉じる',
    'current match': '現在の一致',
    'on line': 'した行',
    // @codemirror/lint
    Diagnostics: 'エラー',
    'No diagnostics': 'エラーなし',
  }

  /**
   * CodeMirror Extensions
   *
   * @see {@link:https://codemirror.net/6/docs/ref/#state.Extension | Extending Editor State}
   */
  extensions: Extension[] = [
    /** @see {@link:https://codemirror.net/6/docs/ref/#basic-setup | basic-setup} */
    basicSetup
  ]

  /**
   * CodeMirror Hook View update event
   *
   * @param update View Update
   *
   * @see {@link https://codemirror.net/6/docs/ref/#view.ViewUpdate|class ViewUpdate}
   */
  onCmUpdate(update: ViewUpdate) {
    console.log(update)
  }
}
```

## LICENSE

[MIT](LICENSE)
