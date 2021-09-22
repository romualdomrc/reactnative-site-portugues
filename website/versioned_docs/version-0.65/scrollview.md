---
id: scrollview
title: ScrollView
---

Componente que envolve a plataforma ScrollView enquanto fornece integração com o sistema "respondedor" de travamento por toque.

Lembre-se de que ScrollViews deve ter uma altura limitada para funcionar, pois eles contêm filhos de altura ilimitada em um contêiner limitado (por meio de uma interação de rolagem). Para limitar a altura de um ScrollView, defina a altura da visualização diretamente (não recomendado) ou certifique-se de que todas as visualizações pai tenham altura limitada. Esquecer de transferir para ```{flex: 1} ``` baixo a pilha de visualização pode levar a erros aqui, que o inspetor de elemento faz a depuração rápida.

Ainda não permite que outros respondentes contidos bloqueiem essa visualização de rolagem de se tornar o respondente. 

Doesn't yet support other contained responders from blocking this scroll view from becoming the responder.

`<ScrollView>` vs [`<FlatList>`](flatlist.md) - qual usar?

`ScrollView` renderiza todos os seus componentes filho de reação de uma vez, mas isso tem uma desvantagem de desempenho.


Imagine que você tem uma lista muito longa de itens que deseja exibir, talvez várias telas de conteúdo. A criação de componentes JS e visualizações nativas para tudo de uma vez, muitos dos quais podem nem mesmo ser mostrados, contribuirá para renderização lenta e aumento do uso de memória.

É aqui que `FlatList` entra em jogo. `FlatList` renderiza itens lentamente, quando eles estão prestes a aparecer, e remove itens que rolam para fora da tela para economizar memória e tempo de processamento.

`FlatList` também é útil se você deseja renderizar separadores entre seus itens, várias colunas, carregamento de rolagem infinita ou qualquer número de outros recursos que ele suporta fora da caixa.

## Example

```SnackPlayer name=ScrollView
import React from 'react';
import { StyleSheet, Text, SafeAreaView, ScrollView, StatusBar } from 'react-native';

const App = () => {
  return (
    <SafeAreaView style={styles.container}>
      <ScrollView style={styles.scrollView}>
        <Text style={styles.text}>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
          minim veniam, quis nostrud exercitation ullamco laboris nisi ut
          aliquip ex ea commodo consequat. Duis aute irure dolor in
          reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
          pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
          culpa qui officia deserunt mollit anim id est laborum.
        </Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
  },
  scrollView: {
    backgroundColor: 'pink',
    marginHorizontal: 20,
  },
  text: {
    fontSize: 42,
  },
});

export default App;
```

---

# Reference

## Props

### [View Props](view.md#props)

Inherits [View Props](view#props).

---

### `StickyHeaderComponent`

Um Componente React que será usado para renderizar cabeçalhos pegajosos deve ser usado junto com `stickyHeaderIndices`. Você pode precisar definir este componente se seu cabeçalho aderente usar transformações personalizadas, por exemplo, quando você deseja que sua lista tenha um cabeçalho animado e que possa ser ocultado. Se o componente não tiver sido fornecido [`ScrollViewStickyHeader`](https://github.com/facebook/react-native/blob/master/Libraries/Components/ScrollView/ScrollViewStickyHeader.js) padrão será usado.

| Type               |
| ------------------ |
| component, element |

---

### `alwaysBounceHorizontal` <div class="label ios">iOS</div>

Quando verdadeiro, a visualização de rolagem salta horizontalmente quando chega ao fim, mesmo se o conteúdo for menor do que a própria visualização de rolagem.

| Type | Default                                               |
| ---- | ----------------------------------------------------- |
| bool | `true` when `horizontal={true}`<hr/>`false` otherwise |

---

### `alwaysBounceVertical` <div class="label ios">iOS</div>

Quando verdadeiro, a visualização de rolagem salta verticalmente quando chega ao final, mesmo se o conteúdo for menor do que a própria visualização de rolagem.

| Type | Default                                             |
| ---- | --------------------------------------------------- |
| bool | `false` when `vertical={true}`<hr/>`true` otherwise |

---

### `automaticallyAdjustContentInsets` <div class="label ios">iOS</div>

Controla se o iOS deve ajustar automaticamente a inserção de conteúdo para visualizações de rolagem que são colocadas atrás de uma barra de navegação ou barra de guias / barra de ferramentas.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `bounces` <div class="label ios">iOS</div>

Quando verdadeiro, a visualização de rolagem salta quando atinge o final do conteúdo se o conteúdo for maior do que a visualização de rolagem ao longo do eixo da direção de rolagem. Quando `false`, desativa todos os saltos, mesmo que os ```alwaysBounce*``` adereços estejam `true`.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `bouncesZoom` <div class="label ios">iOS</div>

Quando `true`, os gestos podem conduzir o zoom além de mín. / Máx. E o zoom será animado para o valor mín. / Máx. No final do gesto, caso contrário, o zoom não excederá os limites.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `canCancelContentTouches` <div class="label ios">iOS</div>

Quando ```false```, uma vez que o rastreamento começa, não tentará arrastar se o toque se mover.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `centerContent` <div class="label ios">iOS</div>

Quando `true`, a visualização de rolagem centraliza automaticamente o conteúdo quando o conteúdo é menor do que os limites da visualização de rolagem; quando o conteúdo é maior do que a visualização de rolagem, esta propriedade não tem efeito.


| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `contentContainerStyle`

Esses estilos serão aplicados ao contêiner de conteúdo da visualização de rolagem que envolve todas as visualizações filhas. 

Exemplo:
 

```
return (
  <ScrollView contentContainerStyle={styles.contentContainer}>
  </ScrollView>
);
...
const styles = StyleSheet.create({
  contentContainer: {
    paddingVertical: 20
  }
});
```

| Type                           |
| ------------------------------ |
| [View Style](view-style-props) |

---

### `contentInset` <div class="label ios">iOS</div>

A quantidade pela qual o conteúdo da visualização de rolagem é inserido nas bordas da visualização de rolagem.

| Type                                                               | Default                                  |
| ------------------------------------------------------------------ | ---------------------------------------- |
| object: {top: number, left: number, bottom: number, right: number} | `{top: 0, left: 0, bottom: 0, right: 0}` |

---

### `contentInsetAdjustmentBehavior` <div class="label ios">iOS</div>

Esta propriedade especifica como as inserções da área de segurança são usadas para modificar a área de conteúdo da visualização de rolagem. Disponível no iOS 11 e posterior.

| Type                                                           | Default   |
| -------------------------------------------------------------- | --------- |
| enum(`'automatic'`, `'scrollableAxes'`, `'never'`, `'always'`) | `'never'` |

---

### `contentOffset`

Usado para definir manualmente o deslocamento de rolagem inicial.

| Type  | Default        |
| ----- | -------------- |
| Point | `{x: 0, y: 0}` |

---

### `decelerationRate`

Um número de ponto flutuante que determina a rapidez com que a visualização de rolagem desacelera depois que o usuário levanta o dedo. Você também pode usar atalhos de string `"normal"``e `"fast"` que correspondam às configurações subjacentes do iOS para `UIScrollViewDecelerationRateNormale` `UIScrollViewDecelerationRateFast` respectivamente.

- `'normal'` 0.998 no iOS, 0.985 no Android.
- `'fast'`, 0.99 no iOS, 0.9 no Android.

| Type                               | Default    |
| ---------------------------------- | ---------- |
| enum(`'fast'`, `'normal'`), number | `'normal'` |

---

### `directionalLockEnabled` <div class="label ios">iOS</div>

Quando verdadeiro, o ScrollView tentará bloquear apenas a rolagem vertical ou horizontal enquanto arrasta.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `disableIntervalMomentum`

Quando verdadeiro, a visualização de rolagem para no próximo índice (em relação à posição de rolagem na liberação), independentemente da velocidade do gesto. Isso pode ser usado para paginação quando a página é menor que a largura do ScrollView horizontal ou a altura do ScrollView vertical.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `disableScrollViewPanResponder`

Quando verdadeiro, o respondedor de pan JS padrão no ScrollView é desabilitado e o controle total sobre os toques dentro do ScrollView é deixado para seus componentes filhos. Isso é particularmente útil se `snapToInterval` estiver ativado, uma vez que não segue os padrões de toque típicos. Não use isso em casos de uso regulares de ScrollView sem, `snapToInterval` pois isso pode causar toques inesperados durante a rolagem.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `endFillColor` <div class="label android">Android</div>

Às vezes, um scrollview ocupa mais espaço do que seu conteúdo preenche. Quando este for o caso, este adereço preencherá o resto do scrollview com uma cor para evitar definir um fundo e criar overdraw desnecessário. Esta é uma otimização avançada que não é necessária no caso geral.

| Type            |
| --------------- |
| [color](colors) |

---

### `fadingEdgeLength` <div class="label android">Android</div>

Esmaece as bordas do conteúdo do pergaminho.

Se o valor for maior que `0`, as bordas de esmaecimento serão definidas de acordo com a direção e posição de rolagem atual, indicando se há mais conteúdo a ser mostrado.

| Type   | Default |
| ------ | ------- |
| number | `0`     |

---

### `horizontal`

Quando `true`, os filhos da visualização de rolagem são organizados horizontalmente em uma linha em vez de verticalmente em uma coluna.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `indicatorStyle` <div class="label ios">iOS</div>

The style of the scroll indicators.

-`'default'` mesmo que `black`.
-`'black'`, o indicador de rolagem é `black`. Esse estilo é bom contra um fundo claro.
-`'white'`, o indicador de rolagem é `white`. Esse estilo é bom contra um fundo escuro.

| Type                                    | Default     |
| --------------------------------------- | ----------- |
| enum(`'default'`, `'black'`, `'white'`) | `'default'` |

---

### `invertStickyHeaders`

Se os cabeçalhos fixos devem ficar na parte inferior em vez de na parte superior do ScrollView. Isso geralmente é usado com ScrollViews invertidos.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `keyboardDismissMode`

Determina se o teclado é dispensado em resposta a um arrasto.

- `'none'`, arrasta não dispensa o teclado.
- `'on-drag'`, o teclado é descartado quando um arrasto começa.

**iOS Only**

- `'interactive'`, o teclado é dispensado interativamente com o arrasto e se move em sincronia com o toque, arrastando para cima cancela a dispensa. No Android, isso não é compatível e terá o mesmo comportamento que 'none'.

| Type                                                                                                                                                            | Default  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| enum(`'none'`, `'on-drag'`) <div className="label android">Android</div><hr />enum(`'none'`, `'on-drag'`, `'interactive'`) <div className="label ios">iOS</div> | `'none'` |

---

### `keyboardShouldPersistTaps`

Determina quando o teclado deve permanecer visível após um toque.

- ´'never'´ tocar fora da entrada de texto em foco quando o teclado está para cima descarta o teclado. Quando isso acontecer, as crianças não receberão a torneira.
- `'always'`´, o teclado não será dispensado automaticamente e a visualização de rolagem não detectará os toques, mas os filhos da visualização de rolagem podem detectar os toques.
- ´'handled'´, o teclado não será dispensado automaticamente quando o toque for manipulado por filhos da visualização de rolagem (ou capturado por um ancestral).
- ´false', obsoleto , use em `'never'` vez disso
- ´true', obsoleto , use em `'always'` vez disso

| Type                                                      | Default   |
| --------------------------------------------------------- | --------- |
| enum(`'always'`, `'never'`, `'handled'`, `false`, `true`) | `'never'` |

---

### `maintainVisibleContentPosition` <div class="label ios">iOS</div>

Quando definida, a visualização de rolagem ajustará a posição de rolagem para que o primeiro filho que está visível no momento e em ou além minIndexForVisiblenão mude de posição. Isso é útil para listas que estão carregando conteúdo em ambas as direções, por exemplo, um tópico de bate-papo, onde novas mensagens podem causar um salto na posição de rolagem. Um valor de 0 é comum, mas outros valores como 1 podem ser usados ​​para pular o carregamento de spinners ou outro conteúdo que não deve manter a posição.

O opcional autoscrollToTopThresholdpode ser usado para fazer o conteúdo rolar automaticamente para o topo após fazer o ajuste, se o usuário estiver dentro do limite do topo antes do ajuste ser feito. Isso também é útil para aplicativos do tipo bate-papo em que você deseja ver as novas mensagens rolarem no lugar, mas não se o usuário rolar para cima algumas maneiras e seria perturbador rolar um monte.

Advertência 1: Reordenar elementos no scrollview com isto habilitado provavelmente causará nervosismo e trepidação. Pode ser consertado, mas atualmente não há planos para fazê-lo. Por enquanto, não reordene o conteúdo de quaisquer ScrollViews ou Listas que usam este recurso.

Advertência 2: isso usa contentOffsete frame.originem código nativo para computar a visibilidade. Oclusão, transformações e outras complexidades não serão levadas em consideração se o conteúdo é "visível" ou não.

| Type                                                                     |
| ------------------------------------------------------------------------ |
| object: { minIndexForVisible: number, autoscrollToTopThreshold: number } |

---

### `maximumZoomScale` <div class="label ios">iOS</div>

A escala de zoom máxima permitida.

| Type   | Default |
| ------ | ------- |
| number | `1.0`   |

---

### `minimumZoomScale` <div class="label ios">iOS</div>

A escala de zoom mínima permitida.

| Type   | Default |
| ------ | ------- |
| number | `1.0`   |

---

### `nestedScrollEnabled` <div class="label android">Android</div>

Ativa a rolagem aninhada para Android API de nível 21+.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `onContentSizeChange`

Chamado quando a visualização de conteúdo rolável de ScrollView muda.

A função de manipulador recebe a largura e a altura do conteúdo como parâmetros: (contentWidth, contentHeight)

É implementado usando o manipulador onLayout anexado ao contêiner de conteúdo que este ScrollView renderiza.

| Type     |
| -------- |
| function |

---

### `onMomentumScrollBegin`

Chamado quando a rolagem de impulso começa (rolagem que ocorre quando ScrollView começa a deslizar).

| Type     |
| -------- |
| function |

---

### `onMomentumScrollEnd`

Chamado quando a rolagem de impulso termina (rolagem que ocorre quando ScrollView desliza para uma parada).

| Type     |
| -------- |
| function |

---

### `onScroll`

Dispara no máximo uma vez por quadro durante a rolagem. A frequência dos eventos pode ser controlada usando o scrollEventThrottleprop. O evento tem a seguinte forma (todos os valores são números):

```js
{
  nativeEvent: {
    contentInset: {bottom, left, right, top},
    contentOffset: {x, y},
    contentSize: {height, width},
    layoutMeasurement: {height, width},
    zoomScale
  }
}
```

| Type     |
| -------- |
| function |

---

### `onScrollBeginDrag`

Chamado quando o usuário começa a arrastar a visualização de rolagem.

| Type     |
| -------- |
| function |

---

### `onScrollEndDrag`

Chamado quando o usuário para de arrastar a visualização de rolagem e ela para ou começa a deslizar.

| Type     |
| -------- |
| function |

---

### `onScrollToTop` <div class="label ios">iOS</div>

Dispara quando a visualização de rolagem rola para o topo após a barra de status ser tocada.

| Type     |
| -------- |
| function |

---

### `overScrollMode` <div class="label android">Android</div>

Usado para substituir o valor padrão do modo overScroll.

Valores possíveis:

- ´'auto'´ - Permita que um usuário role por cima desta visualização apenas se o conteúdo for grande o suficiente para rolar de forma significativa.
-'´'always'´ - Sempre permita que um usuário role por cima esta visualização.
- ´'never'´ - Nunca permita que um usuário role sobre esta visualização.

| Type                                  | Default  |
| ------------------------------------- | -------- |
| enum(`'auto'`, `'always'`, `'never'`) | `'auto'` |

---

### `pagingEnabled`

Quando verdadeiro, a visualização de rolagem para em múltiplos do tamanho da visualização de rolagem durante a rolagem. Isso pode ser usado para paginação horizontal.

> Note: Vertical pagination is not supported on Android.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `persistentScrollbar` <div class="label android">Android</div>

Faz com que as barras de rolagem não fiquem transparentes quando não estão em uso.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `pinchGestureEnabled` <div class="label ios">iOS</div>

Quando verdadeiro, ScrollView permite o uso de gestos de pinça para aumentar e diminuir o zoom.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `refreshControl`

Um componente RefreshControl, usado para fornecer funcionalidade puxar para atualizar para o ScrollView. Funciona apenas para ScrollViews verticais (o horizontal prop deve ser false).

See [RefreshControl](refreshcontrol).

| Type    |
| ------- |
| element |

---

### `removeClippedSubviews`

Experimental: quando true, as visualizações filho fora da tela (cujo overflowvalor é hidden) são removidas de sua supervisão de apoio nativa quando fora da tela. Isso pode melhorar o desempenho da rolagem em listas longas.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `scrollEnabled`

Quando falso, a visualização não pode ser rolada por meio da interação por toque.

Observe que a exibição sempre pode ser rolada chamando `scrollTo`.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `scrollEventThrottle` <div class="label ios">iOS</div>

Isso controla a frequência com que o evento de rolagem será disparado durante a rolagem (como um intervalo de tempo em ms). Um número menor produz melhor precisão para o código que está rastreando a posição de rolagem, mas pode levar a problemas de desempenho de rolagem devido ao volume de informações enviadas pela ponte. Você não notará uma diferença entre os valores definidos entre 1-16, pois o loop de execução JS é sincronizado com a taxa de atualização da tela. Se você não precisa de rastreamento de posição de rolagem preciso, defina este valor mais alto para limitar as informações que estão sendo enviadas através da ponte. O valor padrão é 0, o que resulta no evento de rolagem sendo enviado apenas uma vez a cada vez que a exibição é rolada.

| Type   | Default |
| ------ | ------- |
| number | `0`     |

---

### `scrollIndicatorInsets` <div class="label ios">iOS</div>

A quantidade pela qual os indicadores de visualização de rolagem são inseridos nas bordas da visualização de rolagem. Normalmente deve ser definido com o mesmo valor de `contentInset`.

| Type                                                               | Default                                  |
| ------------------------------------------------------------------ | ---------------------------------------- |
| object: {top: number, left: number, bottom: number, right: number} | `{top: 0, left: 0, bottom: 0, right: 0}` |

---

### `scrollPerfTag` <div class="label android">Android</div>

Tag usada para registrar o desempenho de rolagem nesta visualização de rolagem. Forçará os eventos de momentum a serem ativados (consulte sendMomentumEvents). Isso não faz nada fora da caixa e você precisa implementar um FpsListener nativo personalizado para que seja útil.

| Type   |
| ------ |
| string |

---

### `scrollToOverflowEnabled` <div class="label ios">iOS</div>

Quando `true`, a visualização de rolagem pode ser rolada programaticamente além de seu tamanho de conteúdo.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `scrollsToTop` <div class="label ios">iOS</div>

Quando `true`, a visualização de rolagem rola para o topo quando a barra de status é tocada.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `showsHorizontalScrollIndicator`

Quando true, mostra um indicador de rolagem horizontal..

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `showsVerticalScrollIndicator`

Quando `true`, mostra um indicador de rolagem vertical.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `snapToAlignment` <div class="label ios">iOS</div>

Quando `snapToInterval` definido, snapToAlignmentdefinirá a relação do encaixe com a visualização de rolagem.

Valores possíveis:

- ´'start'´ irá alinhar o snap à esquerda (horizontal) ou superior (vertical).
- ´'center'´ irá alinhar o snap no centro.
- `'end'` irá alinhar o snap à direita (horizontal) ou inferior (vertical).

| Type                                 | Default   |
| ------------------------------------ | --------- |
| enum(`'start'`, `'center'`, `'end'`) | `'start'` |

---

### `snapToEnd`

Use em conjunto com snapToOffsets. Por padrão, o final da lista conta como um deslocamento instantâneo. Defina snapToEndcomo falso para desativar esse comportamento e permitir que a lista role livremente entre seu final e o último snapToOffsetsdeslocamento.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `snapToInterval`

Quando definido, faz com que a visualização de rolagem pare em múltiplos do valor de snapToInterval. Isso pode ser usado para paginar pelos filhos que têm comprimentos menores do que a visualização de rolagem. Normalmente usado em combinação com snapToAlignmente decelerationRate="fast". Substitui pagingEnabledprop menos configurável .

| Type   |
| ------ |
| number |

---

### `snapToOffsets`

Quando definido, faz com que a visualização de rolagem pare nos deslocamentos definidos. Isso pode ser usado para paginar através de filhos de vários tamanhos que têm comprimentos menores do que a visualização de rolagem. Normalmente usado em combinação com decelerationRate="fast". Substitui adereços pagingEnablede menos configuráveis snapToInterval.

| Type            |
| --------------- |
| array of number |

---

### `snapToStart`

Use em conjunto com snapToOffsets. Por padrão, o início da lista conta como um deslocamento instantâneo. Defina snapToStart como falsepara desativar esse comportamento e permitir que a lista role livremente entre o início e o primeiro snapToOffset sdeslocamento.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `stickyHeaderIndices`

Uma matriz de índices filho determinando quais filhos são encaixados na parte superior da tela durante a rolagem. Por exemplo, passar stickyHeaderIndices={[0]}fará com que o primeiro filho seja fixado no topo da visualização de rolagem. Você também pode usar como [x, y, z] para tornar vários itens pegajosos quando eles estão no topo. Esta propriedade não é compatível com horizontal={true}.

| Type            |
| --------------- |
| array of number |

---

### `zoomScale` <div class="label ios">iOS</div>

A escala atual do conteúdo da visualização de rolagem.

| Type   | Default |
| ------ | ------- |
| number | `1.0`   |

---

## Methods

### `flashScrollIndicators()`

```jsx
flashScrollIndicators();
```

Exibe os indicadores de rolagem momentaneamente.


---

### `scrollTo()`

```jsx
scrollTo(
  options?: { x?: number, y?: number, animated?: boolean } | number,
  deprecatedX?: number,
	deprecatedAnimated?: boolean,
);
```

Scrolls to a given x, y offset, either immediately, with a smooth animation.

**Example:**

`scrollTo({ x: 0, y: 0, animated: true })`

> Note: The weird function signature is due to the fact that, for historical reasons, the function also accepts separate arguments as an alternative to the options object. This is deprecated due to ambiguity (y before x), and SHOULD NOT BE USED.

---

### `scrollToEnd()`

```jsx
scrollToEnd(([options]: { animated: boolean, duration: number }));
```

If this is a vertical ScrollView scrolls to the bottom. If this is a horizontal ScrollView scrolls to the right.

Use scrollToEnd({ animated: true })para uma rolagem animada suave, scrollToEnd({ animated: false })para uma rolagem imediata. Para Android, você pode especificar uma duração, por exemplo, scrollToEnd({ duration: 500 })para uma rolagem de duração controlada. Se nenhuma opção for passada, o animatedpadrão é true.
