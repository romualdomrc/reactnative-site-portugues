---
id: textinput
title: TextInput
---

Um componente fundamental para inserir texto no aplicativo por meio de um teclado. As props permitem configurar vários recursos, como correção automática, capitalização automática, texto de espaço reservado e diferentes tipos de teclado, como um teclado numérico.

O caso de uso mais básico é colocar um `TextInput` e utilizar os eventos `onChangeText` para ler a entrada do usuário. Existem também outros eventos, como `OnSubmitEditing` e `OnFocus` que podem ser utilizados. Um exemplo básico:

```SnackPlayer name=TextInput
import React from "react";
import { SafeAreaView, StyleSheet, TextInput } from "react-native";

const UselessTextInput = () => {
  const [text, onChangeText] = React.useState("Useless Text");
  const [number, onChangeNumber] = React.useState(null);

  return (
    <SafeAreaView>
      <TextInput
        style={styles.input}
        onChangeText={onChangeText}
        value={text}
      />
      <TextInput
        style={styles.input}
        onChangeText={onChangeNumber}
        value={number}
        placeholder="useless placeholder"
        keyboardType="numeric"
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  input: {
    height: 40,
    margin: 12,
    borderWidth: 1,
    padding: 10,
  },
});

export default UselessTextInput;
```

Dois métodos que podem ser acessados neste elemento nativo são .focus() e .blur() que atribuem ou retiram o foco do TextInput programaticamente.

Observe que algumas propriedades estão disponíveis apenas com `multiline={true/false}`. Além disso, os estilos de borda que se aplicam a apenas um lado do elemento (por exemplo, `borderBottomColor`, `borderLeftWidth` etc.) não serão aplicados se `multiline=true`. Para obter o mesmo efeito, você pode envolver seu `TextInput` em uma `View`:

```SnackPlayer name=TextInput
import React from 'react';
import { View, TextInput } from 'react-native';

const UselessTextInput = (props) => {
  return (
    <TextInput
      {...props} // Inherit any props passed to it; e.g., multiline, numberOfLines below
      editable
      maxLength={40}
    />
  );
}

const UselessTextInputMultiline = () => {
  const [value, onChangeText] = React.useState('Useless Multiline Placeholder');

  // If you type something in the text box that is a color, the background will change to that
  // color.
  return (
    <View
      style={{
        backgroundColor: value,
        borderBottomColor: '#000000',
        borderBottomWidth: 1,
      }}>
      <UselessTextInput
        multiline
        numberOfLines={4}
        onChangeText={text => onChangeText(text)}
        value={value}
        style={{padding: 10}}
      />
    </View>
  );
}

export default UselessTextInputMultiline;
```

`TextInput` tem, por padrão, uma borda na parte inferior de sua exibição. Essa borda tem seu preenchimento definido pela imagem de fundo fornecida pelo sistema e não pode ser alterado. As soluções para evitar isso são não definir a altura explicitamente; nesse caso, o sistema se encarregará de exibir a borda na posição correta ou não exibir a borda definindo `UnderlineColorAndroid` como transparente.

Observe que no Android, executar a seleção de texto em uma entrada pode alterar o parâmetro da Activity do aplicativo `WindowSoftInputMode` para `AdjustSize`. Isso pode causar problemas com componentes que têm posição: 'absoluto' enquanto o teclado está ativo. Para evitar esse comportamento, especifique `WindowSoftInputMode` em AndroidManifest.xml (https://developer.android.com/guide/topics/manifest/activity-element.html) ou controle esse parâmetro programaticamente com código nativo.

---

# Reference

## Props

### [View Props](view.md#props)

Herda [View Props](view.md#props).

---

### `allowFontScaling`

Especifica se as fontes devem ser dimensionadas de acordo com as configurações de acessibilidade do tamanho do texto. O padrão é `true`.

| Type |
| ---- |
| bool |

---

### `autoCapitalize`

Diz ao `TextInput` para capitalizar automaticamente determinados caracteres. Esta propriedade não é suportada por alguns tipos de teclado, como `name-phone-pad`.

- `characteres`: todos os caracteres.
- `words`: primeira letra de cada palavra.
- `sentences`: primeira letra de cada frase (_default_).
- `none`: não capitalize nada automaticamente.

| Type                                             |
| ------------------------------------------------ |
| enum('none', 'sentences', 'words', 'characters') |

---

### `autoCompleteType` <div class="label android">Android</div>

Especifica dicas de preenchimento automático para o sistema, para que ele possa fornecer preenchimento automático. No Android, o sistema sempre tentará oferecer preenchimento automático usando heurísticas para identificar o tipo de conteúdo. Para desativar o preenchimento automático, defina `AutoCompleteType` para `off`.

Os valores possíveis para `AutoCompleteType` são:

- `off`
- `username`
- `password`
- `email`
- `name`
- `tel`
- `street-address`
- `postal-code`
- `cc-number`
- `cc-csc`
- `cc-exp`
- `cc-exp-month`
- `cc-exp-year`

| Type                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| enum('off', 'username', 'password', 'email', 'name', 'tel', 'street-address', 'postal-code', 'cc-number', 'cc-csc', 'cc-exp', 'cc-exp-month', 'cc-exp-year') |

---

### `autoCorrect`

Se `falso`, desativa a correção automática. O valor padrão é `true`.

| Type |
| ---- |
| bool |

---

### `autoFocus`

Se `true`, focaliza a entrada em `componentDidMount` ou `UseEffect`. O valor padrão é `false`.

| Type |
| ---- |
| bool |

---

### `blurOnSubmit`

Se for `true`, o campo de texto perderá o foco quando enviado. O valor padrão é verdadeiro para campos de linha única e falso para campos de várias linhas. Observe que, para campos de várias linhas, definir `blurOnSubmit` como ` true` significa que pressionar return irá tirar o foco do campo e disparará o evento `onSubmitEditing` em vez de inserir uma nova linha no campo.

| Type |
| ---- |
| bool |

---

### `caretHidden`

Se `verdadeiro`, o cursor está oculto. O valor padrão é `false`.

| Type |
| ---- |
| bool |

---

### `clearButtonMode` <div class="label ios">iOS</div>

Quando o botão Limpar deve aparecer no lado direito da exibição de texto. Essa propriedade é compatível apenas com o componente TextInput de linha única. O valor padrão é `never`.

| Type                                                       |
| ---------------------------------------------------------- |
| enum('never', 'while-editing', 'unless-editing', 'always') |

---

### `clearTextOnFocus` <div class="label ios">iOS</div>

Se `true`, limpa o campo de texto automaticamente quando a edição começar.

| Type |
| ---- |
| bool |

---

### `contextMenuHidden`

Se `true`, o menu de contexto está oculto. O valor padrão é `false`.

| Type |
| ---- |
| bool |

---

### `dataDetectorTypes` <div class="label ios">iOS</div>

Determina os tipos de dados convertidos em URLs clicáveis na entrada de texto. Válido apenas se `multiline= {true} `e `editable= {false}`. Por padrão, nenhum tipo de dados é detectado.

Você pode fornecer um tipo ou uma matriz de vários tipos.

Os valores possíveis para `DataDetectorTypes` são:

- `'phoneNumber'`
- `'link'`
- `'address'`
- `'calendarEvent'`
- `'none'`
- `'all'`

| Type                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enum('phoneNumber', 'link', 'address', 'calendarEvent', 'none', 'all'), ,array of enum('phoneNumber', 'link', 'address', 'calendarEvent', 'none', 'all') |

---

### `defaultValue`

Fornece um valor inicial que mudará quando o usuário começar a digitar. Útil para casos de uso em que você não deseja lidar com a escuta de eventos e atualizar a prop value para manter o estado controlado sincronizado.

| Type   |
| ------ |
| string |

---

### `disableFullscreenUI` <div class="label android">Android</div>

Quando `false`, se houver uma pequena quantidade de espaço disponível em torno de uma entrada de texto (por exemplo, orientação paisagem em um telefone), o sistema operacional pode optar por fazer com que o usuário edite o texto dentro de um modo de entrada de texto em tela cheia. Quando `true`, esse recurso é desativado e os usuários sempre editam o texto diretamente dentro da entrada de texto. O padrão é `false`.

| Type |
| ---- |
| bool |

---

### `editable`

Se `falso`, o texto não é editável. O valor padrão é `true`.

| Type |
| ---- |
| bool |

---

### `enablesReturnKeyAutomatically` <div class="label ios">iOS</div>

Se `true`, o teclado desativa a tecla de retorno quando não há texto e a ativa automaticamente quando há texto. O valor padrão é `false`.

| Type |
| ---- |
| bool |

---

### `importantForAutofill` <div class="label android">Android</div>

Informa ao sistema operacional se os campos individuais em seu aplicativo devem ser incluídos em uma estrutura de visualização para fins de preenchimento automático na API do Android Nível 26+. Os valores possíveis são `auto`, `no`, `noexcludeDescendants`, `yes` e `yesExcludeDescendants`. O valor padrão é `auto`.

- `auto`: Permita que o sistema Android use sua heurística para determinar se a visualização é importante para o preenchimento automático.
- `no`: Essa visualização não é importante para o preenchimento automático.
- `NoExcludeDescendants`: Essa visualização e seus filhos não são importantes para o preenchimento automático.
- `yes`: Essa visualização é importante para o preenchimento automático.
- `YesExcludeDescendants`: Essa visualização é importante para o preenchimento automático, mas seus filhos não são importantes para o preenchimento automático.

| Type                                                                       |
| -------------------------------------------------------------------------- |
| enum('auto', 'no', 'noExcludeDescendants', 'yes', 'yesExcludeDescendants') |

—

### `inlineImageLeft` <div class="label android">Android</div>

Se definido, o recurso de imagem fornecido será renderizado à esquerda. O recurso de imagem deve estar dentro de `/android/app/src/main/res/drawable` e referenciado como

```
<TextInput
 inlineImageLeft='search_icon'
/>
```

| Type   |
| ------ |
| string |

---

### `inlineImagePadding` <div class="label android">Android</div>

Preenchimento entre a imagem embutida, se houver, e a própria entrada de texto.

| Type   |
| ------ |
| number |

---

### `inputAccessoryViewID` <div class="label ios">iOS</div>

Um identificador opcional que vincula um [InputAccessoryView](inputaccessoryview.md) personalizado a essa entrada de texto. O InputAccessoryView é renderizado acima do teclado quando essa entrada de texto recebe o foco.

| Type   |
| ------ |
| string |

---

### `keyboardAppearance` <div class="label ios">iOS</div>

Determina a cor do teclado.

| Type                             |
| -------------------------------- |
| enum('default', 'light', 'dark') |

---

### `keyboardType`

Determina qual teclado abrir, por exemplo, `numeric`.

Veja capturas de tela de todos os tipos [aqui](http://lefkowitz.me/2018/04/30/visual-guide-to-react-native-textinput-keyboardtype-options/).

Os seguintes valores funcionam em todas as plataformas:

- `default`
- `number-pad`
- `decimal-pad`
- `numeric`
- `email-address`
- `phone-pad`

_iOS Only_

Os valores a seguir funcionam somente no iOS:

- `ascii-capable`
- `numbers-and-punctuation`
- `url`
- `name-phone-pad`
- `twitter`
- `web-search`

_Android Only_

Os valores a seguir funcionam apenas no Android:

- `visible-password`

| Type                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enum('default', 'email-address', 'numeric', 'phone-pad', 'ascii-capable', 'numbers-and-punctuation', 'url', 'number-pad', 'name-phone-pad', 'decimal-pad', 'twitter', 'web-search', 'visible-password') |

---

### `maxFontSizeMultiplier`

Especifica a maior escala possível que uma fonte pode alcançar quando `AllowFontScaling` está habilitado. Valores possíveis:

- `null/undefined` (padrão): herdar do nó pai ou do padrão global (0)
- `0`: sem máximo, ignore o padrão pai/global
- `>= 1`: define o `MaxFontSizeMultiplier` deste nó para este valor

| Type   |
| ------ |
| number |

---

### `maxLength`

Limita o número máximo de caracteres que podem ser inseridos. Use isso em vez de implementar a lógica no JS para evitar cintilação.

| Type   |
| ------ |
| number |

---

### `multiline`

Se `true`, a entrada de texto pode ser de várias linhas. O valor padrão é `false`. É importante observar que isso alinha o texto à parte superior do iOS e o centraliza no Android. Use com `TextAlignVertical` definido como `top` para o mesmo comportamento em ambas as plataformas.

| Type |
| ---- |
| bool |

---

### `numberOfLines` <div class="label android">Android</div>

Define o número de linhas para um `TextInput`. Use-o com várias linhas definidas como `true` para poder preencher as linhas.

| Type   |
| ------ |
| number |

---

### `onBlur`

Retorno de chamada chamado quando a entrada de texto perde o foco.

> Nota: Se você estiver tentando acessar o valor `text` de `NativeEvent` tenha em mente que o valor resultante obtido pode ser `undefined`, o que pode causar erros não intencionais. Se você estiver tentando encontrar o último valor de TextInput, você pode usar o evento [`OnEndEditing`](textInput#onendediting), que é acionado após a conclusão da edição.

| Type     |
| -------- |
| function |

---

### `onChange`

Retorno de chamada chamado quando o texto da entrada de texto muda. Isso será chamado com `{nativeEvent: {eventCount, target, text}}`

| Type     |
| -------- |
| function |

---

### `onChangeText`

Método chamado quando o texto da entrada muda. O texto alterado é passado como uma única string para o manipulador do método.

| Type     |
| -------- |
| function |

---

### `onContentSizeChange`

Retorno de chamada chamado quando o tamanho do conteúdo da entrada de texto muda. Isso será chamado com `{NativeEvent: {contentSize: {width, height}}}`.

Chamado apenas para entradas de texto de várias linhas.

| Type     |
| -------- |
| function |

---

### `onEndEditing`

Retorno de chamada quando a entrada de texto termina.

| Type     |
| -------- |
| function |

---

### `onPressIn`

Retorno de chamada quando um toque é ativado.

| Type                     |
| ------------------------ |
| [PressEvent](pressevent) |

---

### `onPressOut`

Retorno de chamada quando um toque é liberado.

| Type                     |
| ------------------------ |
| [PressEvent](pressevent) |

---

### `onFocus`

Retorno de chamada quando a entrada de texto está focada. Isso é chamado com `{NativeEvent: {target}}`.

| Type                                 |
| ------------------------------------ |
| ([LayoutEvent](layoutevent)) => void |

---

### `onKeyPress`

Retorno de chamada quando uma tecla é pressionada. Isso será chamado com `{NativeEvent: {key: keyValue}}` onde `KeyValue` é `'Enter'` ou `'Backspace'` para as respectivas chaves e o caractere digitado de outra forma incluindo `''`para o espaço. Dispara antes de retornos de chamada `OnChange`. Nota: no Android, apenas as entradas do teclado virtual são tratadas, não as entradas do teclado de hardware.

| Type     |
| -------- |
| function |

---

### `onLayout`

Invocado na montagem e nas alterações de layout.

| Type     |
| -------- |
| function |

---

### `onScroll`

Invocado na rolagem de conteúdo com `{nativeEvent: {contentOffset: {x, y}}}`. Também pode conter outras propriedades do ScrollEvent, mas no Android, ContentSize não é fornecido por motivos de desempenho.

| Type     |
| -------- |
| function |

---

### `onSelectionChange`

Retorno de chamada quando a seleção de entrada de texto é alterada. Isso será chamado com `{NativeEvent: {selection: {start, end}}}`. Este prop requer `multiline= {true} `para ser definido.

| Type     |
| -------- |
| function |

---

### `onSubmitEditing`

Retorno de chamada quando o botão enviar da entrada de texto é pressionado com o argumento `{nativeEvent: {text, eventCount, target}}`.

| Type     |
| -------- |
| function |

Observe que, no iOS, esse método não é chamado ao usar `KeyboardType="phone-pad"`.

---

### `placeholder`

A string que será renderizada antes da entrada de texto ter sido inserida.

| Type   |
| ------ |
| string |

---

### `placeholderTextColor`

A cor do texto da string de espaço reservado.

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `returnKeyLabel` <div class="label android">Android</div>

Define a chave de retorno para o rótulo. Use-o em vez de `ReturnKeyType`.

| Type   |
| ------ |
| string |

---

### `returnKeyType`

Determina a aparência da chave de retorno. No Android, você também pode usar `ReturnKeyLabel`.

_Cross platform_

Os seguintes valores funcionam em todas as plataformas:

- `done`
- `go`
- `next`
- `search`
- `send`

_Android Only_

Os valores a seguir funcionam apenas no Android:

- `none`
- `previous`

_iOS Only_

Os valores a seguir funcionam somente no iOS:

- `default`
- `emergency-call`
- `google`
- `join`
- `route`
- `yahoo`

| Type                                                                                                                              |
| --------------------------------------------------------------------------------------------------------------------------------- |
| enum('done', 'go', 'next', 'search', 'send', 'none', 'previous', 'default', 'emergency-call', 'google', 'join', 'route', 'yahoo') |

---

### `rejectResponderTermination` <div class="label ios">iOS</div>

Se `true`, permite que o TextInput passe eventos de toque para o componente pai. Isso permite que componentes como o SwipeableListView possam ser deslizados do TextInput no iOS, como é o caso do Android por padrão. Se `false`, TextInput sempre pede para lidar com a entrada (exceto quando desativado). O valor padrão é `true`.

| Type |
| ---- |
| bool |

---

### `scrollEnabled` <div class="label ios">iOS</div>

Se `falso`, a rolagem da visualização de texto será desativada. O valor padrão é `true`. Funciona apenas com `multiline= {true} `.

| Type |
| ---- |
| bool |

---

### `secureTextEntry`

Se `true`, a entrada de texto obscurece o texto inserido para que textos confidenciais, como senhas, permaneçam seguros. O valor padrão é `false`. Não funciona com `multiline = {true}`.

| Type |
| ---- |
| bool |

---

### `selection`

O início e o fim da seleção da entrada de texto. Defina início e fim com o mesmo valor para posicionar o cursor.

| Type                                |
| ----------------------------------- |
| object: {start: number,end: number} |

---

### `selectionColor`

O realce e a cor do cursor da entrada de texto.

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `selectTextOnFocus`

Se for `true`, todo o texto será automaticamente selecionado em foco.

| Type |
| ---- |
| bool |

---

### `showSoftInputOnFocus`

Quando `falso`, impedirá que o teclado virtual apareça quando o campo estiver focado. O valor padrão é `true`.

| Type |
| ---- |
| bool |

---

### `spellCheck` <div class="label ios">iOS</div>

Se `falso`, desativa o estilo de verificação ortográfica (ou seja, sublinhados vermelhos). O valor padrão é herdado de `AutoCorrect`.

| Type |
| ---- |
| bool |

---

### `textAlign`

Alinhe o texto de entrada aos lados esquerdo, central ou direito do campo de entrada.

Os valores possíveis para `TextAlign` são:

- `left`
- `center`
- `right`

| Type                            |
| ------------------------------- |
| enum('left', 'center', 'right') |

---

### `textContentType` <div class="label ios">iOS</div>

Forneça ao teclado e ao sistema informações sobre o significado semântico esperado para o conteúdo inserido pelos usuários.

Para iOS 11+, você pode definir `TextContentType` para `username` ou` senha` para habilitar o preenchimento automático dos detalhes de login do chaveiro do dispositivo.

Para iOS 12+, `NewPassword` pode ser usado para indicar uma nova entrada de senha que o usuário pode querer salvar no chaveiro, e `OneTimeCode` pode ser usado para indicar que um campo pode ser preenchido automaticamente por um código que chega em um SMS.

Para desativar o preenchimento automático, defina `TextContentType` como `none`.

Os valores possíveis para `TextContentType` são:

- `none`
- `URL`
- `addressCity`
- `addressCityAndState`
- `addressState`
- `countryName`
- `creditCardNumber`
- `emailAddress`
- `familyName`
- `fullStreetAddress`
- `givenName`
- `jobTitle`
- `location`
- `middleName`
- `name`
- `namePrefix`
- `nameSuffix`
- `nickname`
- `organizationName`
- `postalCode`
- `streetAddressLine1`
- `streetAddressLine2`
- `sublocality`
- `telephoneNumber`
- `username`
- `password`
- `newPassword`
- `oneTimeCode`

| Type                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enum('none', 'URL', 'addressCity', 'addressCityAndState', 'addressState', 'countryName', 'creditCardNumber', 'emailAddress', 'familyName', 'fullStreetAddress', 'givenName', 'jobTitle', 'location', 'middleName', 'name', 'namePrefix', 'nameSuffix', 'nickname', 'organizationName', 'postalCode', 'streetAddressLine1', 'streetAddressLine2', 'sublocality', 'telephoneNumber', 'username', 'password') |

---

### `passwordRules` <div class="label ios">iOS</div>

Ao usar `TextContentType` como `NewPassword` no iOS, podemos informar ao sistema operacional os requisitos mínimos da senha para que ela possa gerar uma que os satisfaça. Para criar uma string válida para `PasswordRules`, dê uma olhada no [Apple Docs](https://developer.apple.com/password-rules/).

> Se a caixa de diálogo de geração de senhas não aparecer, certifique-se de que:
>
> > - O preenchimento automático está ativado: **Configurações** → **Senhas e contas** → alterne “Ativar” o**Preenchimento automático de senha**,
>
> - O Chaveiro do iCloud está sendo usado: **Configurações** → **ID Apple** → **iCloud** → **Chave** → alterne “Ligar” o**Chaveiro iCloud**.

| Type   |
| ------ |
| string |

---

### `style`

Observe que nem todos os estilos de texto são suportados, uma lista incompleta do que não é compatível inclui:

- `borderLeftWidth`
- `borderTopWidth`
- `borderRightWidth`
- `borderBottomWidth`
- `borderTopLeftRadius`
- `borderTopRightRadius`
- `borderBottomRightRadius`
- `borderBottomLeftRadius`

consulte [Issue #7070](https://github.com/facebook/react-native/issues/7070) para obter mais detalhes.

[Styles](style.md)

| Type                  |
| --------------------- |
| [Text](text.md#style) |

---

### `textBreakStrategy` <div class="label android">Android</div>

<!-- alex disable simple -->

Defina a estratégia de quebra de texto na API do Android Nível 23+, os valores possíveis são `simple`, `HighQuality`, `balanced` O valor padrão é `simples`.

| Type                                      |
| ----------------------------------------- |
| enum('simple', 'highQuality', 'balanced') |

<!-- alex enable simple -->

---

### `underlineColorAndroid` <div class="label android">Android</div>

A cor do sublinhado `TextInput`.

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `value`

O valor a ser exibido para a entrada de texto. `TextInput` é um componente controlado, o que significa que o valor nativo será forçado a corresponder a essa propriedade de valor, se fornecido. Para a maioria dos usos, isso funciona muito bem, mas em alguns casos isso pode causar cintilação - uma causa comum é impedir edições mantendo o mesmo valor. Além de definir o mesmo valor, defina `editable= {false} `, ou define/atualize `MaxLength` para evitar edições indesejadas sem cintilação.

| Type   |
| ------ |
| string |

## Methods

### `.focus()`

```jsx
focus();
```

Faz a solicitação de entrada nativa receber o foco.

### `.blur()`

```jsx
blur();
```

Faz com que a entrada nativa perca o foco.

### `clear()`

```jsx
clear();
```

Remove todo o texto do `TextInput`.

---

### `isFocused()`

```jsx
isFocused();
```

Retorna `true` se a entrada estiver com o foco no momento; `false` caso contrário.

# Problemas conhecidos

- [react-native #19096](https://github.com/facebook/react-native/issues/19096): Não suporta o `onKeyPreIme` do Android.
- [react-native #19366](https://github.com/facebook/react-native/issues/19366): Chamar .focus () depois de fechar o teclado do Android pelo botão Voltar não traz o teclado novamente.
- [react-native #26799](https://github.com/facebook/react-native/issues/26799): Não suporta `SecureTexentry` do Android quando `keyboardType="email-address"` ou `keyboardType="phone-pad"`.
