---
id: layout-props
title: Layout Props
---

> Exemplos mais detalhados sobre essas propriedades podem ser encontrados na página [Layout com Flexbox] (flexbox).

### Example

O exemplo a seguir mostra como diferentes propriedades podem afetar ou moldar um layout React Native. Você pode tentar, por exemplo, adicionar ou remover quadrados da interface do usuário enquanto altera os valores da propriedade `FlexWrap`.

```SnackPlayer name=LayoutProps%20Example
import React, { useState } from 'react';
import { Button, ScrollView, StatusBar, StyleSheet, Text, View } from 'react-native';

const App = () => {
  const flexDirections = ['row', 'row-reverse', 'column', 'column-reverse'];
  const justifyContents = [
    'flex-start',
    'flex-end',
    'center',
    'space-between',
    'space-around',
    'space-evenly',
  ];
  const alignItemsArr = [
    'flex-start',
    'flex-end',
    'center',
    'stretch',
    'baseline',
  ];
  const wraps = ['nowrap', 'wrap', 'wrap-reverse'];
  const directions = ['inherit', 'ltr', 'rtl'];
  const [flexDirection, setFlexDirection] = useState(0);
  const [justifyContent, setJustifyContent] = useState(0);
  const [alignItems, setAlignItems] = useState(0);
  const [direction, setDirection] = useState(0);
  const [wrap, setWrap] = useState(0);

  const hookedStyles = {
    flexDirection: flexDirections[flexDirection],
    justifyContent: justifyContents[justifyContent],
    alignItems: alignItemsArr[alignItems],
    direction: directions[direction],
    flexWrap: wraps[wrap],
  };

  const changeSetting = (value, options, setterFunction) => {
    if (value == options.length - 1) {
      setterFunction(0);
      return;
    }
    setterFunction(value + 1);
  };
  const [squares, setSquares] = useState([<Square />, <Square />, <Square />]);
  return (
    <>
      <View style={{ paddingTop: StatusBar.currentHeight }} />
      <View style={[styles.container, styles.playingSpace, hookedStyles]}>
        {squares.map(elem => elem)}
      </View>
      <ScrollView style={[styles.container]}>
        <View style={[styles.controlSpace]}>
          <View style={styles.buttonView}>
            <Button
              title="Change Flex Direction"
              onPress={() =>
                changeSetting(flexDirection, flexDirections, setFlexDirection)
              }
            />
            <Text style={styles.text}>{flexDirections[flexDirection]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Justify Content"
              onPress={() =>
                changeSetting(
                  justifyContent,
                  justifyContents,
                  setJustifyContent
                )
              }
            />
            <Text style={styles.text}>{justifyContents[justifyContent]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Align Items"
              onPress={() =>
                changeSetting(alignItems, alignItemsArr, setAlignItems)
              }
            />
            <Text style={styles.text}>{alignItemsArr[alignItems]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Direction"
              onPress={() => changeSetting(direction, directions, setDirection)}
            />
            <Text style={styles.text}>{directions[direction]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Change Flex Wrap"
              onPress={() => changeSetting(wrap, wraps, setWrap)}
            />
            <Text style={styles.text}>{wraps[wrap]}</Text>
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Add Square"
              onPress={() => setSquares([...squares, <Square/>])}
            />
          </View>
          <View style={styles.buttonView}>
            <Button
              title="Delete Square"
              onPress={() =>
                setSquares(squares.filter((v, i) => i != squares.length - 1))
              }
            />
          </View>
        </View>
      </ScrollView>
    </>
  );
};

const styles = StyleSheet.create({
  container: {
    height: '50%',
  },
  playingSpace: {
    backgroundColor: 'white',
    borderColor: 'blue',
    borderWidth: 3,
  },
  controlSpace: {
    flexDirection: 'row',
    flexWrap: 'wrap',
    backgroundColor: '#F5F5F5',
  },
  buttonView: {
    width: '50%',
    padding: 10,
  },
  text: { textAlign: 'center' },
});

const Square = () => (
  <View style={{
    width: 50,
    height: 50,
    backgroundColor: randomHexColor(),
  }} />
);

const randomHexColor = () => {
  return '#000000'.replace(/0/g, () => {
    return (~~(Math.random() * 16)).toString(16);
  });
};

export default App;
```

---

# Reference

## Props

### `alignContent`

`AlignContent` controla como as linhas se alinham na direção cruzada, substituindo o `AlignContent` do pai. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/align-content para obter mais detalhes.

| Type                                                                                 | Required |
| ------------------------------------------------------------------------------------ | -------- |
| enum('flex-start', 'flex-end', 'center', 'stretch', 'space-between', 'space-around') | No       |

---

### `alignItems`

`AlignItems` alinha as crianças na direção cruzada. Por exemplo, se os filhos estiverem fluindo verticalmente, `AlignItems` controla como eles se alinham horizontalmente. Funciona como `align-items` em CSS (padrão: stretch). Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/align-items para obter mais detalhes.

| Type                                                            | Required |
| --------------------------------------------------------------- | -------- |
| enum('flex-start', 'flex-end', 'center', 'stretch', 'baseline') | No       |

---

### `alignSelf`

`AlignSelf` controla como um filho se alinha na direção cruzada, substituindo os `AlignItems` do pai. Funciona como `align-self` em CSS (padrão: auto). Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/align-self para obter mais detalhes.

| Type                                                                    | Required |
| ----------------------------------------------------------------------- | -------- |
| enum('auto', 'flex-start', 'flex-end', 'center', 'stretch', 'baseline') | No       |

---

### `aspectRatio`

A proporção controla o tamanho da dimensão indefinida de um nó. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio para obter mais detalhes.

- Em um nó com uma largura/altura definida, a proporção controla o tamanho da dimensão não definida
- Em um nó com uma base flexível definida, a taxa de proporção controla o tamanho do nó no eixo transversal se não definido
- Em um nó com uma função de medida, a proporção de aspecto funciona como se a função de medida mede a base flexível
- Em um nó com crescimento flexível/encolhimento, a proporção controla o tamanho do nó no eixo transversal se não definido
- A proporção leva em consideração as dimensões mín/máx.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderBottomWidth`

`BorderBottomWidth` funciona como `border-bottom-width` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/border-bottom-width para obter mais detalhes.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderEndWidth`

Quando a direção é `ltr`, `BorderRendWidth` é equivalente a `BorderRightWidth`. Quando a direção é `rtl`, `BorderEndWidth` é equivalente a `BorderLeftWidth`.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderLeftWidth`

`BorderLeftWidth` funciona como `border-left-width` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/border-left-width para obter mais detalhes.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderRightWidth`

`borderRightWidth` works like `border-right-width` in CSS. See https://developer.mozilla.org/en-US/docs/Web/CSS/border-right-width for more details.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderStartWidth`

Quando a direção é `ltr`, `BorderStartWidth` é equivalente a `BorderLeftWidth`. Quando a direção é `rtl`, `BorderStartWidth` é equivalente a `BorderRightWidth`.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderTopWidth`

`BorderTopWidth` funciona como `border-top-width` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/border-top-width para obter mais detalhes.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `borderWidth`

`BorderWidth` funciona como `border-width` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/border-width para obter mais detalhes.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `bottom`

`bottom` é o número de pixels lógicos para deslocar a borda inferior deste componente.

Funciona de forma semelhante ao `bottom` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/bottom para obter mais detalhes sobre como o `bottom` afeta o layout.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `direction`

`direção` especifica o fluxo direcional da interface do usuário. O padrão é `herd`, exceto para o nó raiz que terá valor com base na localidade atual. Consulte https://yogalayout.com/docs/layout-direction para obter mais detalhes.

| Type                          | Required | Platform |
| ----------------------------- | -------- | -------- |
| enum('inherit', 'ltr', 'rtl') | No       | iOS      |

---

### `display`

`display` define o tipo de exibição deste componente.

Funciona de forma semelhante a `display` em CSS, mas suporta apenas 'flex' e 'none'. 'flex' é o padrão.

| Type                 | Required |
| -------------------- | -------- |
| enum('none', 'flex') | No       |

---

### `end`

Quando a direção é `ltr`, `end` é equivalente a `direita`. Quando a direção é `rtl`, `end` é equivalente a `esquerda`.

Esse estilo tem precedência sobre os estilos `esquerda` e `direita`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `flex`

No React Native, `flex` não funciona da mesma forma que no CSS. `flex` é um número em vez de uma string, e funciona de acordo com o mecanismo de layout [Yoga] (https://github.com/facebook/yoga).

Quando `flex` é um número positivo, ele torna o componente flexível e será dimensionado proporcional ao seu valor flexível. Portanto, um componente com `flex` definido como 2 terá o dobro do espaço que um componente com `flex` definido como 1. `flex: <positive number>` equivale a `FlexGrow: <positive number>, FlexShrink: 1, FlexBasis: 0`.

Quando `flex` é 0, o componente é dimensionado de acordo com `largura` e `altura`, e é inflexível.

Quando `flex` é -1, o componente é normalmente dimensionado de acordo com `largura` e `altura`. No entanto, se não houver espaço suficiente, o componente diminuirá para sua `minWidth` e `minHeight`.

`FlexGrow`, `FlexShrink` e `FlexBasis` funcionam da mesma forma que no CSS.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `flexBasis`

`FlexBasis` é uma forma independente de eixo de fornecer o tamanho padrão de um item ao longo do eixo principal. Definir o `FlexBasis` de um filho é semelhante a definir a `largura` desse filho se seu pai for um contêiner com `FlexDirection: linha` ou definir a `altura` de um filho se seu pai for um contêiner com `FlexDirection: coluna`. O `FlexBasis` de um item é o tamanho padrão desse item, o tamanho do item antes de qualquer cálculo `FlexGrow` e `FlexShrink` serem executados.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `flexDirection`

`FlexDirection` controla quais direções os filhos de um contêiner vão. `linha` vai da esquerda para a direita, `coluna` vai de cima para baixo, e você pode adivinhar o que os outros dois fazem. Funciona como `flex-direction` em CSS, exceto que o padrão é `column`. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction para obter mais detalhes.

| Type                                                   | Required |
| ------------------------------------------------------ | -------- |
| enum('row', 'row-reverse', 'column', 'column-reverse') | No       |

---

### `flexGrow`

`FlexGrow` descreve como qualquer espaço dentro de um contêiner deve ser distribuído entre seus filhos ao longo do eixo principal. Depois de colocar seus filhos, um contêiner distribuirá qualquer espaço restante de acordo com os valores de crescimento flexível especificados por seus filhos.

`FlexGrow` aceita qualquer valor de ponto flutuante >= 0, sendo 0 o valor padrão. Um contêiner distribuirá qualquer espaço restante entre seus filhos, ponderado pelos valores `FlexGrow` dos filhos.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `flexShrink`

[`FlexShrink`] (layout-props #flexshrink) descreve como encolher filhos ao longo do eixo principal no caso em que o tamanho total dos filhos transborda o tamanho do contêiner no eixo principal. `FlexShrink` é muito semelhante ao `FlexGrow` e pode ser pensado da mesma forma se qualquer tamanho de transbordamento for considerado um espaço restante negativo. Essas duas propriedades também funcionam bem juntas, permitindo que as crianças cresçam e encolham conforme necessário.

`FlexShrink` aceita qualquer valor de ponto flutuante >= 0, sendo 1 o valor padrão. Um contêiner encolherá seus filhos ponderados pelos valores `FlexShrink` dos filhos.

| Type   | Required |
| ------ | -------- |
| number | No       |

---

### `flexWrap`

`FlexWrap` controla se as crianças podem se envolver depois de atingirem o final de um contêiner flexível. Funciona como `flex-wrap` em CSS (padrão: nowrap). Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap para obter mais detalhes. Observe que ele não funciona mais com `AligniEms: stretch` (o padrão), então você pode querer usar `AligniEms: flex-start`, por exemplo (detalhes de mudança de quebra: https://github.com/facebook/react-native/releases/tag/v0.28.0).

| Type                                   | Required |
| -------------------------------------- | -------- |
| enum('wrap', 'nowrap', 'wrap-reverse') | No       |

---

### `height`

`height` sets the height of this component.

Funciona de forma semelhante a `altura` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/height para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `justifyContent`

`JustifyContent` alinha as crianças na direção principal. Por exemplo, se os filhos estiverem fluindo verticalmente, `JustifyContent` controla como eles se alinham verticalmente. Funciona como `justify-content` em CSS (padrão: flex-start). Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content para obter mais detalhes.

| Type                                                                                      | Required |
| ----------------------------------------------------------------------------------------- | -------- |
| enum('flex-start', 'flex-end', 'center', 'space-between', 'space-around', 'space-evenly') | No       |

---

### `left`

`esquerda` é o número de pixels lógicos para deslocar a borda esquerda deste componente.

Funciona de forma semelhante a `left` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/left para obter mais detalhes sobre como a `esquerda` afeta o layout.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `margin`

Definir `margin` tem o mesmo efeito que definir cada um de `MarginTop`, `MarginLeft`, `MarginBottom` e `MarginRight`. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/margin para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginBottom`

`MarginBottom` funciona como `margin-bottom` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/margin-bottom para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginEnd`

Quando a direção é `ltr`, `MarginEnd` é equivalente a `MarginRight`. Quando a direção é `rtl`, `MarginEnd` é equivalente a `MarginLeft`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginHorizontal`

Definir `MarginHorizontal` tem o mesmo efeito que definir `MarginLeft` e `MarginRight`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginLeft`

`MarginLeft` funciona como `margin-left` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/margin-left para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginRight`

`MarginRight` funciona como `margin-right` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/margin-right para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginStart`

Quando a direção é `ltr`, `MarginStart` é equivalente a `MarginLeft`. Quando a direção é `rtl`, `MarginStart` é equivalente a `MarginRight`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginTop`

`MarginTop` funciona como `margin-top` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/margin-top para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `marginVertical`

Definir `MarginVertical` tem o mesmo efeito que definir `MarginTop` e `MarginBottom`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `maxHeight`

`maxHeight` é a altura máxima para este componente, em pixels lógicos.

Funciona de forma semelhante a `max-height` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/max-height para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `maxWidth`

`MaxWidth` é a largura máxima deste componente, em pixels lógicos.

Funciona de forma semelhante a `max-width` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/max-width para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `minHeight`

`minHeight` é a altura mínima para este componente, em pixels lógicos.

Funciona de forma semelhante a `min-height` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/min-height para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `minWidth`

`minWidth` é a largura mínima para este componente, em pixels lógicos.

Funciona de forma semelhante à `min-width` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/min-width para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `overflow`

`overflow` controla como as crianças são medidas e exibidas. `overflow: hidden` faz com que as visualizações sejam cortadas enquanto `overflow: scroll` faz com que as visualizações sejam medidas independentemente do eixo principal de seus pais. Funciona como `overflow` em CSS (padrão: visível). Consulte https://developer.mozilla.org/en/docs/Web/CSS/overflow para obter mais detalhes.

| Type                                | Required |
| ----------------------------------- | -------- |
| enum('visible', 'hidden', 'scroll') | No       |

---

### `padding`

Definir `padding` tem o mesmo efeito que definir cada um de `PaddingTop`, `PaddingBottom`, `PaddingLeft` e `PaddingRight`. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/padding para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingBottom`

`PaddingBottom` funciona como `padding-bottom` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/padding-bottom para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingEnd`

Quando a direção é `ltr`, `PaddingEnd` é equivalente a `PaddingRight`. Quando a direção é `rtl`, `PaddingEnd` é equivalente a `PaddingLeft`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingHorizontal`

Definir `PaddingHorizontal` é como definir `PaddingLeft` e `PaddingRight`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingLeft`

`PaddingLeft` funciona como `padding-left` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/padding-left para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingRight`

`PaddingRight` funciona como `padding-right` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/padding-right para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingStart`

Quando a direção é `ltr`, `PaddingStart` é equivalente a `PaddingLeft`. Quando a direção é `rtl`, `PaddingStart` é equivalente a `PaddingRight`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `paddingTop`

`paddingTop` funciona como `padding-top` em CSS. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/padding-top para obter mais detalhes.

| Type            | Required |
| --------------- | -------- |
| number, ,string | No       |

---

### `paddingVertical`

Definir `PaddingVertical` é como definir `PaddingTop` e `PaddingBottom`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `position`

`posição` no React Native é semelhante ao CSS normal, mas tudo é definido como `relativo` por padrão, então o posicionamento `absoluto` é sempre relativo ao pai.

Se você quiser posicionar um filho usando números específicos de pixels lógicos em relação ao pai, defina o filho para ter uma posição `absoluta`.

Se você quiser posicionar um filho em relação a algo que não é o pai, não use estilos para isso. Use a árvore de componentes.

Consulte https://github.com/facebook/yoga para obter mais detalhes sobre como a `posição` difere entre o React Native e o CSS.

| Type                         | Required |
| ---------------------------- | -------- |
| enum('absolute', 'relative') | No       |

---

### `right`

`right` é o número de pixels lógicos para deslocar a borda direita deste componente.

Funciona de forma semelhante a `right` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/right para obter mais detalhes sobre como `right` afeta o layout.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `start`

Quando a direção é `ltr`, `start` é equivalente a `esquerda`. Quando a direção é `rtl`, `start` é equivalente a `right`.

Esse estilo tem precedência sobre os estilos `esquerda`, `direita` e `final`.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `top`

`top` é o número de pixels lógicos para deslocar a borda superior deste componente.

Funciona de forma semelhante ao `top` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis.

Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/top para obter mais detalhes sobre como o `top` afeta o layout.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `width`

`width` define a largura deste componente.

Funciona de forma semelhante à `largura` no CSS, mas no React Native você deve usar pontos ou porcentagens. Ems e outras unidades não são compatíveis. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/width para obter mais detalhes.

| Type           | Required |
| -------------- | -------- |
| number, string | No       |

---

### `zIndex`

`ZIndex` controla quais componentes são exibidos em cima dos outros. Normalmente, você não usa `ZIndex`. Os componentes são renderizados de acordo com sua ordem na árvore de documentos, de modo que os componentes posteriores se sobrepõem aos anteriores. `ZIndex` pode ser útil se você tiver animações ou interfaces modais personalizadas nas quais não deseja esse comportamento.

Funciona como a propriedade CSS `z-index` - componentes com um `ZIndex` maior serão renderizados no topo. Pense na direção z como se estivesse apontando do telefone para o globo ocular. Consulte https://developer.mozilla.org/en-US/docs/Web/CSS/z-index para obter mais detalhes.

No iOS, `ZIndex` pode exigir que `View`s sejam irmãos um do outro para que funcione conforme o esperado.

| Type   | Required |
| ------ | -------- |
| number | No       |

---
