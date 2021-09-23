---
id: text
title: Text
---

importar guias de '@ theme / Tabs'; importar TabItem de '@ theme / TabItem'; importar constantes de '@ site / core / TabsConstants';

Um componente React para exibir texto.

`Text` oferece suporte a aninhamento, estilo e manipulação de toque.

No exemplo a seguir, o título aninhado e o texto do corpo herdarão `fontFamily` de` styles.baseText`, mas o título fornece seus próprios estilos adicionais. O título e o corpo serão empilhados um sobre o outro devido às novas linhas literais: 
<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Text%20Functional%20Component%20Example
import React, { useState } from "react";
import { Text, StyleSheet } from "react-native";

const TextInANest = () => {
  const [titleText, setTitleText] = useState("Bird's Nest");
  const bodyText = "This is not really a bird nest.";

  const onPressTitle = () => {
    setTitleText("Bird's Nest [pressed]");
  };

  return (
    <Text style={styles.baseText}>
      <Text style={styles.titleText} onPress={onPressTitle}>
        {titleText}
        {"\n"}
        {"\n"}
      </Text>
      <Text numberOfLines={5}>{bodyText}</Text>
    </Text>
  );
};

const styles = StyleSheet.create({
  baseText: {
    fontFamily: "Cochin"
  },
  titleText: {
    fontSize: 20,
    fontWeight: "bold"
  }
});

export default TextInANest;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Text%20Class%20Component%20Example
import React, { Component } from "react";
import { Text, StyleSheet } from "react-native";

class TextInANest extends Component {
  constructor(props) {
    super(props);
    this.state = {
      titleText: "Bird's Nest",
      bodyText: "This is not really a bird nest."
    };
  }

  onPressTitle = () => {
    this.setState({ titleText: "Bird's Nest [pressed]" });
  };

  render() {
    return (
      <Text style={styles.baseText}>
        <Text
          style={styles.titleText}
          onPress={this.onPressTitle}
        >
          {this.state.titleText}
          {"\n"}
          {"\n"}
        </Text>
        <Text numberOfLines={5}>{this.state.bodyText}</Text>
      </Text>
    );
  }
}

const styles = StyleSheet.create({
  baseText: {
    fontFamily: "Cochin"
  },
  titleText: {
    fontSize: 20,
    fontWeight: "bold"
  }
});

export default TextInANest;
```

</TabItem>
</Tabs>

## Nested text

Tanto o Android quanto o iOS permitem que você exiba texto formatado anotando intervalos de uma string com formatação específica, como texto em negrito ou colorido (`NSAttributedString` no iOS,` SpannableString` no Android). Na prática, isso é muito tedioso. Para React Native, decidimos usar o paradigma da web para isso, onde você pode aninhar o texto para obter o mesmo efeito. 

```SnackPlayer name=Nested%20Text%20Example
import React from 'react';
import { Text, StyleSheet } from 'react-native';

const BoldAndBeautiful = () => {
  return (
    <Text style={styles.baseText}>
      I am bold
      <Text style={styles.innerText}> and red</Text>
    </Text>
  );
};

const styles = StyleSheet.create({
  baseText: {
    fontWeight: 'bold'
  },
  innerText: {
    color: 'red'
  }
});

export default BoldAndBeautiful;
```

Behind the scenes, React Native converts this to a flat `NSAttributedString` or `SpannableString` that contains the following information:

```jsx
"I am bold and red"
0-9: bold
9-17: bold, red
```

## Containers

O elemento `<Text>` é único em relação ao layout: tudo dentro não está mais usando o layout Flexbox, mas usando o layout de texto. Isso significa que os elementos dentro de um `<Text>` não são mais retângulos, mas quebram quando veem o final da linha. 

```jsx
<Text>
  <Text>First part and </Text>
  <Text>second part</Text>
</Text>
// Text container: the text will be inline if the space allowed it
// |First part and second part|

// otherwise, the text will flow as if it was one
// |First part |
// |and second |
// |part       |

<View>
  <Text>First part and </Text>
  <Text>second part</Text>
</View>
// View container: each text is its own block
// |First part and|
// |second part   |

// otherwise, the text will flow in its own block
// |First part |
// |and        |
// |second part|
```

## Limited Style Inheritance

O elemento `<Text>` é único em relação ao layout: tudo dentro não está mais usando o layout Flexbox, mas usando o layout de texto. Isso significa que os elementos dentro de um `<Text>` não são mais retângulos, mas quebram quando veem o final da linha. 

```css
html {
  font-family: 'lucida grande', tahoma, verdana, arial, sans-serif;
  font-size: 11px;
  color: #141823;
}
```

Todos os elementos do documento herdarão essa fonte, a menos que eles ou um de seus pais especifique uma nova regra.

No React Native, somos mais rígidos sobre isso: ** você deve envolver todos os nós de texto dentro de um componente `<Text>` **. Você não pode ter um nó de texto diretamente sob um `<View>`. 

```jsx
// BAD: will raise exception, can't have a text node as child of a <View>
<View>
  Some text
</View>

// GOOD
<View>
  <Text>
    Some text
  </Text>
</View>
```

Você também perde a capacidade de configurar uma fonte padrão para uma subárvore inteira. Enquanto isso, `fontFamily` só aceita um único nome de fonte, que é diferente de` font-family` em CSS. A maneira recomendada de usar fontes e tamanhos consistentes em seu aplicativo é criar um componente `MyAppText` que os inclui e usar este componente em seu aplicativo. Você também pode usar este componente para criar componentes mais específicos como `MyAppHeaderText` para outros tipos de texto. 

```jsx
<View>
  <MyAppText>
    Text styled with the default font for the entire application
  </MyAppText>
  <MyAppHeaderText>Text styled as a header</MyAppHeaderText>
</View>
```

Supondo que `MyAppText` seja um componente que apenas renderiza seus filhos em um componente` Text` com estilo, então `MyAppHeaderText` pode ser definido da seguinte maneira: 

```jsx
class MyAppHeaderText extends Component {
  render() {
    return (
      <MyAppText>
        <Text style={{ fontSize: 20 }}>
          {this.props.children}
        </Text>
      </MyAppText>
    );
  }
}
```

Compor `MyAppText` dessa forma garante que obteremos os estilos de um componente de nível superior, mas nos deixa a capacidade de adicioná-los / sobrescrevê-los em casos de uso específicos.

React Native ainda tem o conceito de herança de estilo, mas limitado a subárvores de texto. Neste caso, a segunda parte estará em negrito e vermelho. 

```jsx
<Text style={{ fontWeight: 'bold' }}>
  I am bold
  <Text style={{ color: 'red' }}>and red</Text>
</Text>
```

Acreditamos que esta forma mais restrita de estilizar o texto resultará em aplicativos melhores:

- (Desenvolvedor) Os componentes do React são projetados com forte isolamento em mente: Você deve ser capaz de soltar um componente em qualquer lugar em seu aplicativo, confiando que, desde que os adereços sejam os mesmos, ele terá a mesma aparência e se comportará da mesma maneira. As propriedades de texto que poderiam herdar de fora dos adereços quebrariam esse isolamento.

- (Implementador) A implementação do React Native também é simplificada. Não precisamos ter um campo `fontFamily` em cada elemento, e não precisamos potencialmente atravessar a árvore até a raiz cada vez que exibimos um nó de texto. A herança de estilo só é codificada dentro do componente Texto nativo e não vaza para outros componentes ou para o próprio sistema. 

---

# Reference

## Props

### `accessibilityHint`

Uma dica de acessibilidade ajuda os usuários a entender o que acontecerá quando eles executarem uma ação no elemento de acessibilidade quando esse resultado não estiver claro no rótulo de acessibilidade. 

| Type   |
| ------ |
| string |

---

### `accessibilityLabel`

Substitui o texto lido pelo leitor de tela quando o usuário interage com o elemento. Por padrão, o rótulo é construído percorrendo todos os filhos e acumulando todos os nós `Texto` separados por espaço.

| Tipo |
| ------ |
| string |

---

### `accessibilityRole`

Diz ao leitor de tela para tratar o elemento focado no momento como tendo uma função específica.

No iOS, essas funções são mapeadas para as características de acessibilidade correspondentes. O botão de imagem tem a mesma funcionalidade como se o traço fosse definido para 'imagem' e 'botão'. Consulte o [Guia de acessibilidade] (accessibility.md # accessibilitytraits-ios) para obter mais informações.

No Android, essas funções têm funcionalidade semelhante no TalkBack, como adicionar características de acessibilidade no Voiceover no iOS

| Tipo |
| -------------------------------------------------- - |
| [AccessibilityRole] (accessibility # accessibilityrole) |

---

### `accessibilityState`

Diz ao leitor de tela para tratar o elemento focado no momento como se estivesse em um estado específico.

Você pode fornecer um estado, nenhum estado ou vários estados. Os estados devem ser transmitidos por meio de um objeto. Ex: `{selected: true, disabled: true}`.

| Tipo |
| -------------------------------------------------- ---- |
| [AccessibilityState] (acessibilidade # accessibilitystate) |

---

### `acessível`

Quando definido como `true`, indica que a visualização é um elemento de acessibilidade.

Consulte o [Guia de acessibilidade] (acessibilidade # acessível-ios-android) para obter mais informações.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `true` |

---

### `adjustsFontSizeToFit`

Especifica se as fontes devem ser reduzidas automaticamente para se ajustar às restrições de estilo fornecidas.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

---

### `allowFontScaling`

Especifica se as fontes devem ser dimensionadas para respeitar as configurações de acessibilidade do tamanho do texto.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `true` |

---

### `android_hyphenationFrequency` <div class =" label android "> Android </div>

Define a frequência de hifenização automática a ser usada ao determinar quebras de palavras na API Android nível 23+.

| Tipo | Padrão |
| ------------------------------------------------ | -------- |
| enum (`'none'`,`' full'`, `'balance'`,`' high'`) | `'none'` |

---

### `dataDetectorType` <div class =" label android "> Android </div>

Determina os tipos de dados convertidos em URLs clicáveis ​​no elemento de texto. Por padrão, nenhum tipo de dados é detectado.

Você pode fornecer apenas um tipo.

| Tipo | Padrão |
| -------------------------------------------------- ----------- | -------- |
| enum (`'phoneNumber'`,`' link'`, `'email'`,`' none'`, `'all'`) | `'none'` |

---

### `disabled` <div class =" label android "> Android </div>

Especifica o estado desativado da visualização de texto para fins de teste.

| Tipo | Padrão |
| ---- | ------- |
| bool | `false` |

---

### `ellipsizeMode`

Quando `numberOfLines` é definido, este prop define como o texto será truncado. `numberOfLines` deve ser definido em conjunto com este prop.

Pode ser um dos seguintes valores:

- `head` - A linha é exibida de forma que o final caiba no contêiner e o texto ausente no início da linha é indicado por um glifo de reticências. por exemplo, "... wxyz"
- `meio` - A linha é exibida de forma que o início e o fim caibam no contêiner e o texto ausente no meio é indicado por um glifo de reticências. "ab ... sim"
- `cauda` - A linha é exibida de forma que o início se ajuste ao contêiner e o texto ausente no final da linha seja indicado por um glifo de reticências. por exemplo, "abcd ..."
- `clip` - As linhas não são desenhadas além da borda do contêiner de texto. 

> No Android, quando `numberOfLines` é definido com um valor superior a` 1`, apenas o valor `tail` funcionará corretamente.

| Tipo | Padrão |
| ---------------------------------------------- | ------- |
| enum (`'head'`,`' middle'`, `'tail'`,`' clip'`) | `tail` |

---

### `maxFontSizeMultiplier`

Especifica a maior escala possível que uma fonte pode atingir quando `allowFontScaling` está habilitado. Valores possíveis:

- `null / undefined`: herdar do nó pai ou do padrão global (0)
- `0`: sem máx, ignorar padrão pai / global
- `> = 1`: define o` maxFontSizeMultiplier` deste nó para este valor

| Tipo | Padrão |
| ------ | ----------- |
| número | `undefined` |

---

### `minimumFontScale` <div class =" label ios "> iOS </div>

Especifica a menor escala possível que uma fonte pode atingir quando `adjustsFontSizeToFit` está habilitado. (valores 0,01-1,0).

| Tipo |
| ------ |
| número |

---

### `nativeID`

Usado para localizar esta visualização do código nativo.

| Tipo |
| ------ |
| string |

---

### `numberOfLines`

Usado para truncar o texto com reticências após calcular o layout do texto, incluindo quebra de linha, de forma que o número total de linhas não exceda esse número. Definir essa propriedade como `0` resultará na desconfiguração desse valor, o que significa que nenhuma restrição de linhas será aplicada.

Este prop é comumente usado com `ellipsizeMode`.

| Tipo | Padrão |
| ------ | ------- |
| número | `0` |

---

### `onLayout`

Chamado na montagem e nas mudanças de layout.

| Tipo |
| -------------------------------------------------- --- |
| ({nativeEvent: [LayoutEvent] (layoutevent)}) => void |

---

### `onLongPress`

Esta função é chamada ao pressionar longamente.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

---

### `onMoveShouldSetResponder`

Esta visualização deseja "reivindicar" capacidade de resposta ao toque? Isso é chamado para cada movimento de toque em `View` quando não é o respondedor.

| Tipo |
| -------------------------------------------------- ---- |
| ({nativeEvent: [PressEvent] (pressevent)}) => boolean |

---

### `onPress`

Esta função é chamada ao pressionar.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

---

### `onResponderGrant`

O View agora está respondendo a eventos de toque. Este é o momento de destacar e mostrar ao usuário o que está acontecendo.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

---

### `onResponderMove`

O usuário está movendo o dedo.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

---

### `onResponderRelease`

Disparado no final do toque.

| Tipo |
| -------------------------------------------------- - |
| ({nativeEvent: [PressEvent] (pressevent)}) => void |

---

### `onResponderTerminate`

O respondente foi retirado do `View`. Pode ser levado por outras visualizações após uma chamada para `onResponderTerminationRequest`, ou pode ser levado pelo sistema operacional sem perguntar (por exemplo, acontece com o centro de controle / centro de notificação no iOS) 

| Type                                                |
| --------------------------------------------------- |
| ({ nativeEvent: [PressEvent](pressevent) }) => void |

---

### `onResponderTerminationRequest`

Algum outro `View` deseja se tornar um respondedor e está pedindo a este` View` para liberar seu respondente. Retornar `true` permite sua liberação.

| Tipo |
| -------------------------------------------------- ---- |
| ({nativeEvent: [PressEvent] (pressevent)}) => boolean |

---

### `onStartShouldSetResponderCapture`

Se um `View` pai deseja evitar que um` View` filho se torne um respondedor em uma inicialização por toque, ele deve ter este manipulador que retorna `true`.

| Tipo |
| -------------------------------------------------- ---- |
| ({nativeEvent: [PressEvent] (pressevent)}) => boolean |

---

### `onTextLayout`

Chamado na mudança de layout do texto.

| Tipo |
| -------------------------------------------------- - |
| ([`TextLayoutEvent`] (text # textlayoutevent)) => mixed |

---

### `pressRetentionOffset`

Quando a visualização de rolagem está desabilitada, isso define o quão longe o seu toque pode sair do botão, antes de desativar o botão. Uma vez desativado, tente movê-lo para trás e você verá que o botão é reativado novamente! Mova-o para a frente e para trás várias vezes enquanto a visualização de rolagem está desativada. Certifique-se de passar uma constante para reduzir as alocações de memória.

| Tipo |
| -------------------- |
| [Rect] (rect), número |

---

### `selecionável`

Permite que o usuário selecione o texto, para usar a funcionalidade de copiar e colar nativa.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

---

### `selectionColor` <div class =" label android "> Android </div>

A cor de destaque do texto.

| Tipo |
| --------------- |
| [cor] (cores) |

---

### `style`

| Tipo |
| -------------------------------------------------- ------------------ |
| [Estilo de texto] (adereços de estilo de texto), [Ver adereços de estilo] (ver adereços de estilo) |

---

### `suppressHighlighting` <div class =" label ios "> iOS </div>

Quando `true`, nenhuma mudança visual é feita quando o texto é pressionado. Por padrão, um oval cinza destaca o texto ao pressionar para baixo.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

---

### `testID`

Usado para localizar essa visualização em testes de ponta a ponta.

| Tipo |
| ------ |
| string |

---

### `textBreakStrategy` <div class =" label android "> Android </div>

Defina a estratégia de quebra de texto na API Android Nível 23+, os valores possíveis são `simples`,` altaQualidade`, `equilibrado`.

| Tipo | Padrão |
| ----------------------------------------------- | ------------- |
| enum (`'simple'`,`' highQuality'`, `'balance'`) | `highQuality` |

## Definições de tipo

### TextLayout

O objeto `TextLayout` é uma parte do retorno de chamada [` TextLayoutEvent`] (text # textlayoutevent) e contém os dados de medição para a linha `Text`.

#### Exemplo

`` `js
{
    capHeight: 10.496,
    ascender: 14.624,
    descendente: 4,
    largura: 28,224,
    altura: 18.624,
    xHeight: 6.048,
    x: 0,
    y: 0
}
`` `

#### Propriedades

| Nome Tipo | Opcional | Descrição
| --------- | ------ | -------- | -------------------------------------------------- ----------------- |
| ascender | número | Não A altura ascendente da linha após as alterações do layout do texto. |
| capHeight | número | Não Altura da letra maiúscula acima da linha de base. |
| descender | número | Não A altura descendente da linha após as alterações do layout do texto. |
| altura | número | Não Altura da linha após as alterações do layout do texto. |
| largura | número | Não Largura da linha após as alterações do layout do texto. |
| x | número | Não Coordenada da linha X dentro do componente Texto. |
| xHeight | número | Não Distância entre a linha de base e a mediana da linha (tamanho do corpo). |
| y | número | Não Coordenada da linha Y dentro do componente Texto. |

### TextLayoutEvent

O objeto `TextLayoutEvent` é retornado no retorno de chamada como resultado de uma mudança no layout do componente. Ele contém uma chave chamada `lines` com um valor que é um array contendo o objeto [` TextLayout`] (text # textlayout) correspondente a cada linha de texto renderizada.

#### Exemplo

`` `js
{
  linhas: [
    TextLayout,
    TextLayout
    // ...
  ];
  alvo: 1127;
}
`` `

#### Propriedades

| Nome Tipo | Opcional | Descrição
| ------ | --------------------------------------- | -------- | -------------------------------------------------- --- |
| linhas | matriz de [TextLayout] (text # textlayout) s | Não Fornece os dados TextLayout para cada linha renderizada. |
| alvo | número | Não O id do nó do elemento. | 
