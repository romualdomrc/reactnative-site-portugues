---
id: view
title: View
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

O componente mais fundamental para construir uma UI, `View` é um contêiner que suporta layout com controles [flexbox](flexbox.md), [style](style.md), [algum tratamento de toque](handling-touches.md) e [acessibilidade](accessibility.md). `View` mapeia diretamente para a visualização nativa equivalente em qualquer plataforma em que o React Native esteja sendo executado, seja um `UIView`, `<div>`, `android.view`, etc.

`View` foi projetado para ser aninhado dentro de outras visualizações e pode ter de nenhum a muitos filhos de qualquer tipo.

Este exemplo cria uma `View` que envolve duas caixas com cor e um componente de texto em uma linha com preenchimento.

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=View%20Function%20Component%20Example
import React from "react";
import { View, Text } from "react-native";

const ViewBoxesWithColorAndText = () => {
  return (
    <View
      style={{
        flexDirection: "row",
        height: 100,
        padding: 20
      }}
    >
      <View style={{ backgroundColor: "blue", flex: 0.3 }} />
      <View style={{ backgroundColor: "red", flex: 0.5 }} />
      <Text>Hello World!</Text>
    </View>
  );
};

export default ViewBoxesWithColorAndText;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=View%20Class%20Component%20Example
import React, { Component } from "react";
import { View, Text } from "react-native";

class App extends Component {
  render() {
    return (
      <View
        style={{
          flexDirection: "row",
          height: 100,
          padding: 20
        }}
      >
        <View style={{ backgroundColor: "blue", flex: 0.3 }} />
        <View style={{ backgroundColor: "red", flex: 0.5 }} />
        <Text>Hello World!</Text>
      </View>
    );
  }
}

export default App;
```

</TabItem>
</Tabs>

> `View`s são projetados para serem usados com [`StyleSheet`](style.md) para maior clareza e desempenho, embora estilos embutidos também sejam suportados.

### Synthetic Touch Events

Para adereços de resposta `View` (por exemplo, `OnResponderMove`), o evento de toque sintético passado para eles está na forma de [PressEvent](pressevent).

---

# Referência

## Props

### `onStartShouldSetResponder`

Essa visualização quer se tornar um respondedor no início de um toque?

`View.props.onStartShouldSetResponder: (event) => [true | false]`, onde `event` ' um' [PressEvent](pressevent).

| Type     | Obrigatório |
| -------- | ----------- |
| function | No          |

---

### `accessible`

Quando `true`, indica que a visualização é um elemento de acessibilidade. Por padrão, todos os elementos tocáveis estão acessíveis.

| Type | Required |
| ---- | -------- |
| bool | No       |

---

### `accessibilityLabel`

Substitui o texto lido pelo leitor de tela quando o usuário interage com o elemento. Por padrão, o rótulo é construído atravessando todos os filhos e acumulando todos os nós `Texto` separados por espaço.

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `accessibilityHint`

Uma dica de acessibilidade ajuda os usuários a entender o que acontecerá quando eles executarem uma ação no elemento de acessibilidade quando esse resultado não estiver claro no rótulo de acessibilidade.

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `accessibilityRole`

`AccessibilityRole` comunica o propósito de um componente ao usuário de uma tecnologia assistiva.

`AccessibilityRole` pode ser um dos seguintes:

- `'none'` - Usado quando o elemento não tem função.
- `'button'` - Usado quando o elemento deve ser tratado como um botão.
- `'link'` - Usado quando o elemento deve ser tratado como um link.
- `'search'` - Usado quando o elemento do campo de texto também deve ser tratado como um campo de pesquisa.
- `'image'` - Usada quando o elemento deve ser tratado como uma imagem. Pode ser combinado com botão ou link, por exemplo.
- `'keyboardkey'` - Usado quando o elemento atua como uma tecla do teclado.
- `'text'` - Usado quando o elemento deve ser tratado como texto estático que não pode mudar.
- `'adjustable'` - Usado quando um elemento pode ser “ajustado” (por exemplo, um controle deslizante).
- `'imagebutton'` - Usado quando o elemento deve ser tratado como um botão e também é uma imagem.
- `'header'` - Usado quando um elemento atua como um cabeçalho para uma seção de conteúdo (por exemplo, o título de uma barra de navegação).
- `'summary'` - Usado quando um elemento pode ser usado para fornecer um resumo rápido das condições atuais no aplicativo quando o aplicativo é iniciado pela primeira vez.
- `'alert'` - Usado quando um elemento contém texto importante a ser apresentado ao usuário.
- `'checkbox'` - Usado quando um elemento representa uma caixa de seleção que pode ser marcada, desmarcada ou ter um estado verificado misto.
- `'combobox'` - Usado quando um elemento representa uma caixa de combinação, que permite ao usuário selecionar entre várias opções.
- `'menu'` - Usado quando o componente é um menu de escolhas.
- `'menubar'` - Usado quando um componente é um contêiner de vários menus.
- `'menuitem'` - Usado para representar um item dentro de um menu.
- `'progressbar'` - Usado para representar um componente que indica o progresso de uma tarefa.
- `'radio'` - Usado para representar um botão de rádio.
- `'radiogroup'` - Usado para representar um grupo de botões de opção.
- `'scrollbar'` - Usado para representar uma barra de rolagem.
- `'spinbutton'` - Usado para representar um botão que abre uma lista de opções.
- `'switch'` - Usado para representar um interruptor que pode ser ligado e desligado.
- `'tab'` - Usado para representar uma guia.
- `'tablist'` - Usado para representar uma lista de guias.
- `'timer'` - Usado para representar um temporizador.
- `'toolbar'` - Usada para representar uma barra de ferramentas (um contêiner de botões de ação ou componentes).

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `accessibilityState`

Descreve o estado atual de um componente para o usuário de uma tecnologia assistiva.

Consulte o [Guia de acessibilidade](accessibility.md#accessibilitystate-ios-android) para obter mais informações.

| Type                                                                                           | Required |
| ---------------------------------------------------------------------------------------------- | -------- |
| object: {disabled: bool, selected: bool, checked: bool or 'mixed', busy: bool, expanded: bool} | No       |

---

### `accessibilityValue`

Representa o valor atual de um componente. Pode ser uma descrição textual do valor de um componente ou, para componentes baseados em intervalo, como controles deslizantes e barras de progresso, contém informações de intervalo (mínimo, atual e máximo).

Consulte o [Guia de acessibilidade](accessibility.md#accessibilityvalue-ios-android) para obter mais informações.

| Type                                                          | Required |
| ------------------------------------------------------------- | -------- |
| object: {min: number, max: number, now: number, text: string} | No       |

---

### `accessibilityActions`

As ações de acessibilidade permitem que uma tecnologia assistiva invoque programaticamente as ações de um componente. A propriedade `AccessibilityActions` deve conter uma lista de objetos de ação. Cada objeto de ação deve conter o nome do campo e o rótulo.

Consulte o [Guia de acessibilidade](accessibility.md#accessibility-actions) para obter mais informações.

| Type  | Required |
| ----- | -------- |
| array | No       |

---

### `onAccessibilityAction`

Invocado quando o usuário executa as ações de acessibilidade. O único argumento para essa função é um evento que contém o nome da ação a ser executada.

Consulte o [Guia de acessibilidade](accessibility.md#accessibility-actions) para obter mais informações.

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onAccessibilityTap`

Quando `accessible` for verdadeiro, o sistema tentará invocar essa função quando o usuário executar o gesto de toque de acessibilidade.

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onMagicTap`

Quando `accessible` for `true`, o sistema invocará essa função quando o usuário executar o gesto de toque mágico.

| Type     | Required | Platform |
| -------- | -------- | -------- |
| function | No       | iOS      |

---

### `onAccessibilityEscape`

Quando `accessible` for `true`, o sistema invocará essa função quando o usuário executar o gesto de escape.

| Type     | Required | Platform |
| -------- | -------- | -------- |
| function | No       | iOS      |

---

### `accessibilityViewIsModal`

Um valor que indica se o VoiceOver deve ignorar os elementos nas visualizações que são irmãos do receptor. O padrão é `false`.

Consulte o [Guia de acessibilidade](accessibility.md#accessibilityviewismodal-ios) para obter mais informações.

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | iOS      |

---

### `accessibilityElementsHidden`

Um valor que indica se os elementos de acessibilidade contidos nesse elemento de acessibilidade estão ocultos. O padrão é `false`.

Consulte o [Guia de acessibilidade](accessibility.md#accessibilityelementshidden-ios) para obter mais informações.

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | iOS      |

---

### `accessibilityIgnoresInvertColors`

Um valor que indica essa exibição deve ou não ser invertido quando a inversão de cores estiver ativada. Um valor de `true` dirá à exibição para não ser invertida, mesmo se a inversão de cores estiver ativada.

Consulte o [Guia de acessibilidade](accessibility.md#accessibilityignoresinvertcolors) para obter mais informações.

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | iOS      |

---

### `accessibilityLiveRegion`

Indica aos serviços de acessibilidade se o usuário deve ser notificado quando essa exibição for alterada. Funciona apenas para a API do Android >= 19. Valores possíveis:

- `'none'` - Os serviços de acessibilidade não devem anunciar alterações nessa exibição.
- `'polite'`- Os serviços de acessibilidade devem anunciar mudanças nessa visão.
- `'assertive'` - Accessibility services should interrupt ongoing speech to immediately announce changes to this view.

Consulte os documentos [Android `View`](http://developer.android.com/reference/android/view/View.html#attr_android:accessibilityLiveRegion) para referência.

| Type                                | Required | Platform |
| ----------------------------------- | -------- | -------- |
| enum('none', 'polite', 'assertive') | No       | Android  |

---

### `importantForAccessibility`

Controla como a exibição é importante para a acessibilidade, ou seja, se ela dispara eventos de acessibilidade e se for relatada aos serviços de acessibilidade que consultam a tela. Funciona apenas para Android.

Valores possíveis:

- `'auto'` - O sistema determina se a visualização é importante para acessibilidade - padrão (recomendado).
- `'yes'` - A visão é importante para acessibilidade.
- `'no'` - The view is not important for accessibility.
- `'no-hide-descendants'` - A visão não é importante para acessibilidade, nem nenhuma de suas visões descendentes.

Consulte os documentos [Android `ImportantForAccessibility`](http://developer.android.com/reference/android/R.attr.html#importantForAccessibility) para referência.

| Type                                             | Required | Platform |
| ------------------------------------------------ | -------- | -------- |
| enum('auto', 'yes', 'no', 'no-hide-descendants') | No       | Android  |

---

### `hitSlop`

Isso define até que ponto um evento de toque pode começar longe da exibição. As diretrizes de interface típicas recomendam alvos de toque que tenham pelo menos 30 a 40 pontos/pixels independentes de densidade.

Por exemplo, se uma visualização tocável tiver uma altura de 20, a altura tocável pode ser estendida para 40 com `HitSlop={{top: 10, bottom: 10, left: 0, right: 0}}`

> A área de toque nunca ultrapassa os limites de visualização pai e o índice Z das visualizações de irmãos sempre terá precedência se um toque atingir duas exibições sobrepostas.

| Type                                                               | Required |
| ------------------------------------------------------------------ | -------- |
| object: {top: number, left: number, bottom: number, right: number} | No       |

---

### `nativeID`

Usado para localizar essa exibição de classes nativas.

> Isso desativa a otimização de 'remoção de exibição somente layout' para essa visualização!

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `onLayout`

Invocado na montagem e nas alterações de layout.

Esse evento é acionado imediatamente após o layout ter sido calculado, mas o novo layout pode ainda não ser refletido na tela no momento em que o evento é recebido, especialmente se uma animação de layout estiver em andamento.

| Type                                 | Required |
| ------------------------------------ | -------- |
| ([LayoutEvent](layoutevent)) => void | No       |

---

### `onMoveShouldSetResponder`

Essa exibição quer “reivindicar” a capacidade de resposta ao toque? Isso é chamado para cada movimento de toque no `View` quando não é o respondente.

`View.props.onMoveShouldSetResponder: (event) => [true | false] `, onde `event` é um [PresseEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onMoveShouldSetResponderCapture`

Se um `View` pai quiser impedir que um filho `View` se torne respondedor em um movimento, ele deve ter esse manipulador que retorna `true`.

`View.props.onMoveShouldSetResponderCapture: (event) => [true | false] `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onResponderGrant`

O View agora está respondendo por eventos de toque. Este é o momento de destacar e mostrar ao usuário o que está acontecendo.

`View.props.onResponderGrant: (event) => {} `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onResponderMove`

O usuário está movendo o dedo.

`View.props.onResponderMove: (event) => {} `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onResponderReject`

Outro respondedor já está ativo e não o liberará para essa `View` pedindo para ser o respondente.

`View.props.onResponderReject: (event) => {} `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onResponderRelease`

Dado no final do toque.

`View.props.onResponderRelease: (event) => {} `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onResponderTerminate`

O respondente foi retirado do `View`. Pode ser obtida por outras visualizações após uma chamada para `onResponderTerminationRequest`, ou pode ser feita pelo sistema operacional sem perguntar (por exemplo, acontece com o centro de controle/ centro de notificações no iOS)

`View.props.onResponderTerminate: (event) => {} `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onResponderTerminationRequest`

Algum outro `View` quer se tornar respondedor e está pedindo a este `View` para liberar seu respondedor. Retornar `true` permite seu lançamento.

`View.props.onResponderTerminationRequest: (event) => {} `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onStartShouldSetResponderCapture`

Se um `View` pai quiser impedir que um filho `View` se torne respondente em um início de toque, ele deve ter esse manipulador que retorna `true`.

`View.props.onStartShouldSetResponderCapture: (event) => [true | false] `, onde `event` é um [PressEvent] (pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `pointerEvents`

Controla se a `View` pode ser o alvo de eventos de toque.

- `'auto'`: A Visualização pode ser o alvo de eventos de toque.
- `'none'`: A Visualização nunca é alvo de eventos de toque.
- `'box-none'`: A Visualização nunca é alvo de eventos de toque, mas suas subvisualizações podem ser. Ele se comporta como se a exibição tivesse as seguintes classes em CSS:

```
.box-none {
     pointer-events: none;
}
.box-none * {
     pointer-events: auto;
}
```

- `'box-only'`: A exibição pode ser o alvo de eventos de toque, mas suas subvisualizações não podem ser. Ele se comporta como se a exibição tivesse as seguintes classes em CSS:

```
.box-only {
     pointer-events: auto;
}
.box-only * {
     pointer-events: none;
}
```

> Como `PointerEvents` não afeta layout/aparência, e já estamos nos desviando da especificação adicionando modos adicionais, optamos por não incluir `PointerEvents` em `style`. Em algumas plataformas, precisaríamos implementá-lo como um `ClassName` de qualquer maneira. Usar `style` ou não é um detalhe de implementação da plataforma.

| Type                                         | Required |
| -------------------------------------------- | -------- |
| enum('box-none', 'none', 'box-only', 'auto') | No       |

---

### `removeClippedSubviews`

Esta é uma propriedade de desempenho reservada exposta por `RCTView` e é útil para rolar o conteúdo quando há muitas subvisualizações, a maioria das quais fora da tela. Para que essa propriedade seja efetiva, ela deve ser aplicada a uma exibição que contenha muitas subviews que se estendem fora de seu limite. As subvisualizações também devem ter `overflow: hidden`, assim como a visualização que contém (ou uma de suas superviews).

| Type | Required |
| ---- | -------- |
| bool | No       |

---

### `style`

| Type                              | Required |
| --------------------------------- | -------- |
| [View Style](view-style-props.md) | No       |

---

### `testID`

Usado para localizar essa exibição em testes de ponta a ponta.

> Isso desativa a otimização de 'remoção de exibição somente layout' para essa visualização!

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `collapsable`

As exibições que são usadas apenas para fazer o layout de seus filhos ou não desenham nada podem ser removidas automaticamente da hierarquia nativa como uma otimização. Defina esta propriedade como `false` para desativar essa otimização e garantir que essa `View` exista na hierarquia de visualizações nativa.

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | Android  |

---

### `needsOffscreenAlphaCompositing`

Se essa `View` precisa ser renderizada fora da tela e composta com um alfa para preservar cores 100% corretas e o comportamento de mesclagem. O padrão (`false`) volta para desenhar o componente e seus filhos com um alfa aplicado à tinta usada para desenhar cada elemento em vez de renderizar o componente completo fora da tela e compor de volta com um valor alfa. Esse padrão pode ser perceptível e indesejado no caso em que a `View` em que você está definindo uma opacidade tem vários elementos sobrepostos (por exemplo, várias `View`s sobrepostas ou texto e um plano de fundo).

A renderização fora da tela para preservar o comportamento alfa correto é extremamente cara e difícil de depurar para desenvolvedores não nativos, e é por isso que ela não está ativada por padrão. Se você precisar habilitar essa propriedade para uma animação, considere combiná-la com RenderToHardwareTextureAndroid se a visualização**conteúdo** for estática (ou seja, não precisa ser redesenhada a cada quadro). Se essa propriedade estiver habilitada, essa View será renderizada fora da tela uma vez, salva em uma textura de hardware e, em seguida, composta na tela com um alfa a cada quadro sem precisar alternar os destinos de renderização na GPU.

| Type | Required |
| ---- | -------- |
| bool | No       |

---

### `renderToHardwareTextureAndroid`

Se essa `View` deve renderizar a si mesma (e todos os seus filhos) em uma única textura de hardware na GPU.

No Android, isso é útil para animações e interações que modificam apenas opacidade, rotação, tradução e/ou escala: nesses casos, a exibição não precisa ser redesenhada e as listas de exibição não precisam ser reexecutadas. A textura pode ser reutilizada e recomposta com diferentes parâmetros. A desvantagem é que isso pode usar memória de vídeo limitada, portanto, essa prop deve ser ajustada novamente para false no final da interação/animação.

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | Android  |

---

### `shouldRasterizeIOS`

Se essa `View` deve ser renderizada como um bitmap antes da composição.

No iOS, isso é útil para animações e interações que não modificam as dimensões desse componente nem seus filhos; por exemplo, ao traduzir a posição de uma exibição estática, a rasterização permite que o renderizador reutilize um bitmap armazenado em cache de uma exibição estática e compô-lo rapidamente durante cada quadro.

A rasterização incorre em uma passagem de desenho fora da tela e o bitmap consome memória. Teste e meça ao usar essa propriedade.

| Type | Required | Platform |
| ---- | -------- | -------- |
| bool | No       | iOS      |

---

### `nextFocusDown`

Designa a próxima exibição para receber foco quando o usuário navegar para baixo. Consulte a [documentação do Android](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusDown).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusForward`

Designa a próxima exibição para receber o foco quando o usuário navegar para frente. Consulte a [documentação do Android](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusForward).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusLeft`

Designa a próxima exibição para receber o foco quando o usuário navegar para a esquerda. Consulte a [documentação do Android](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusLeft).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusRight`

Designa a próxima exibição para receber o foco quando o usuário navega para a direita. Consulte a [documentação do Android](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusRight).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `nextFocusUp`

Designa a próxima exibição para receber foco quando o usuário navegar para cima. Consulte a [documentação do Android](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusUp).

| Type   | Required | Platform |
| ------ | -------- | -------- |
| number | No       | Android  |

---

### `focusable`

Se esta `View` deve ser focalizável com um dispositivo de entrada sem toque, por exemplo, receba foco com um teclado de hardware.

| Type    | Required | Platform |
| ------- | -------- | -------- |
| boolean | No       | Android  |
