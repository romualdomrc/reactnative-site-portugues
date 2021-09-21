---
id: touchablewithoutfeedback
title: TouchableWithoutFeedback
---

> Se você está procurando uma maneira mais abrangente e preparada para o futuro de lidar com a entrada baseada em toque, confira a API [Pressable](pressable.md).

Não use, a menos que você tenha um bom motivo. Todos os elementos que respondem à interface devem ter um feedback visual quando tocados.

`TouchableWithoutFeedback` suporta apenas um filho. Se você deseja ter vários componentes filhos, envolva-os em uma `View`. É importante ressaltar que `TouchableWithoutFeedback` funciona clonando seu filho e aplicando propriedades de resposta a ele. Portanto, é necessário que quaisquer componentes intermediários passem essas props para o componente React Native subjacente.

## Padrão de uso

```jsx
function MyComponent(props) {
  return (
    <View {...props} style={{ flex: 1, backgroundColor: '#fff' }}>
      <Text>My Component</Text>
    </View>
  );
}

<TouchableWithoutFeedback onPress={() => alert('Pressed!')}>
  <MyComponent />
</TouchableWithoutFeedback>;
```

## Exemplo

```SnackPlayer name=TouchableWithoutFeedback
import React, { useState } from "react";
import { StyleSheet, TouchableWithoutFeedback, Text, View } from "react-native";

const TouchableWithoutFeedbackExample = () => {
  const [count, setCount] = useState(0);

  const onPress = () => {
    setCount(count + 1);
  };

  return (
    <View style={styles.container}>
      <View style={styles.countContainer}>
        <Text style={styles.countText}>Count: {count}</Text>
      </View>
      <TouchableWithoutFeedback onPress={onPress}>
        <View style={styles.button}>
          <Text>Touch Here</Text>
        </View>
      </TouchableWithoutFeedback>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingHorizontal: 10
  },
  button: {
    alignItems: "center",
    backgroundColor: "#DDDDDD",
    padding: 10
  },
  countContainer: {
    alignItems: "center",
    padding: 10
  },
  countText: {
    color: "#FF00FF"
  }
});

export default TouchableWithoutFeedbackExample;
```

---

# Reference

## Props

### `accessibilityIgnoresInvertColors`

| Type    | Required |
| ------- | -------- |
| Boolean | No       |

---

### `accessible`

Quando `true`, indica que a visualização é um elemento de acessibilidade. Por padrão, todos os elementos tocáveis estão acessíveis.

| Type | Required |
| ---- | -------- |
| bool | No       |

---

### `accessibilityLabel`

Substitui o texto lido pelo leitor de tela quando o usuário interage com o elemento. Por padrão, o rótulo é construído atravessando todos os filhos e acumulando todos os nós `Text` separados por espaço.

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `accessibilityHint`

Uma dica de acessibilidade ajuda os usuários a entender o que acontecerá quando eles executarem uma ação no elemento quando esse resultado não estiver claro no rótulo.

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

### `accessibilityValue`

Representa o valor atual de um componente. Pode ser uma descrição textual do valor de um componente ou, para componentes baseados em intervalo, como controles deslizantes e barras de progresso, contém informações de intervalo (mínimo, atual e máximo).

Consulte o [Guia de acessibilidade](accessibility.md#accessibilityvalue-ios-android) para obter mais informações.

| Type                                                          | Required |
| ------------------------------------------------------------- | -------- |
| object: {min: number, max: number, now: number, text: string} | No       |

---

### `delayLongPress`

Duração (em milissegundos) de `OnPressIn` antes de `OnLongPress` ser chamado.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `delayPressIn`

Duração (em milissegundos), desde o início do toque, antes de `OnPressIn` ser chamado.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `delayPressOut`

Duração (em milissegundos), a partir do lançamento do toque, antes de `onPressOut` ser chamado.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `disabled`

Se verdadeiro, desative todas as interações para esse componente.

| Type | Required |
| ---- | -------- |
| bool | No       |

---

### `hitSlop`

Isso define o quão longe o toque pode começar a partir do botão. Isso é adicionado a `PressRetentionOffset` ao sair do botão.

> A área de toque nunca ultrapassa os limites de visualização pai e o índice Z das visualizações de irmãos sempre terá precedência se um toque atingir duas exibições sobrepostas.

| Type                   | Required |
| ---------------------- | -------- |
| [Rect](rect) or number | No       |

### `onBlur`

Invocado quando o item perde o foco.

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onFocus`

Invocado quando o item recebe foco.

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onLayout`

Invocado na montagem e nas alterações de layout.

| Type                                 | Required |
| ------------------------------------ | -------- |
| ([LayoutEvent](layoutevent)) => void | No       |

---

### `onLongPress`

Chamado se o tempo após `OnPressIn` durar mais de 370 milissegundos. Esse período de tempo pode ser personalizado com [`DelayLongPress`] (#delaylongpress).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onPress`

Chamado quando o toque é liberado, mas não se cancelado (por exemplo, por um pergaminho que rouba o bloqueio do respondente). O primeiro argumento de função é um evento na forma de [PressEvent](pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onPressIn`

Chamado assim que o elemento tocável é pressionado e invocado antes mesmo do OnPress. Isso pode ser útil ao fazer solicitações de rede. O primeiro argumento de função é um evento na forma de [PressEvent](pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `onPressOut`

Chamado assim que o toque é lançado antes mesmo do OnPress. O primeiro argumento de função é um evento na forma de [PressEvent](pressevent).

| Type     | Required |
| -------- | -------- |
| function | No       |

---

### `pressRetentionOffset`

Quando a visualização de rolagem está desativada, isso define até que ponto o toque pode se mover para fora do botão, antes de desativar o botão. Depois de desativado, tente movê-lo de volta e você verá que o botão é reativado novamente! Mova-o para frente e para trás várias vezes enquanto a visualização de rolagem estiver desativada. Certifique-se de passar uma constante para reduzir as alocações de memória.

| Type                   | Required |
| ---------------------- | -------- |
| [Rect](rect) or number | No       |

---

### `nativeID`

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `testID`

Usado para localizar essa exibição em testes de ponta a ponta.

| Type   | Required |
| ------ | -------- |
| string | No       |

---

### `touchSoundDisabled`

Se for verdade, não reproduz um som do sistema ao toque.

| Type    | Required | Platform |
| ------- | -------- | -------- |
| Boolean | No       | Android  |
