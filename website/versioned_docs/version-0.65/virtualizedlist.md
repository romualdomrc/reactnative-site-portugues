---
id: virtualizedlist
title: VirtualizedList
---

Implementação básica para os componentes mais convenientes [`<FlatList>`] (flatlist.md) e [`<SectionList>`] (sectionlist.md), que também são melhor documentados. Em geral, isso só deve ser usado se você precisar de mais flexibilidade do que [`FlatList`] (flatlist.md) fornece, por exemplo, para uso com dados imutáveis em vez de matrizes simples.

A virtualização melhora enormemente o consumo de memória e o desempenho de listas grandes, mantendo uma janela de renderização finita de itens ativos e substituindo todos os itens fora da janela de renderização por um espaço em branco de tamanho adequado. A janela se adapta ao comportamento de rolagem, e os itens são renderizados incrementalmente com baixo preço (após qualquer interação em execução) se estiverem longe da área visível, ou com hi-pri de outra forma para minimizar o potencial de ver espaço em branco.

## Exemplo

```SnackPlayer name=VirtualizedListExample
import React from 'react';
import { SafeAreaView, View, VirtualizedList, StyleSheet, Text, StatusBar } from 'react-native';

const DATA = [];

const getItem = (data, index) => ({
  id: Math.random().toString(12).substring(0),
  title: `Item ${index+1}`
});

const getItemCount = (data) => 50;

const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);

const App = () => {
  return (
    <SafeAreaView style={styles.container}>
      <VirtualizedList
        data={DATA}
        initialNumToRender={4}
        renderItem={({ item }) => <Item title={item.title} />}
        keyExtractor={item => item.key}
        getItemCount={getItemCount}
        getItem={getItem}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight,
  },
  item: {
    backgroundColor: '#f9c2ff',
    height: 150,
    justifyContent: 'center',
    marginVertical: 8,
    marginHorizontal: 16,
    padding: 20,
  },
  title: {
    fontSize: 32,
  },
});

export default App;
```

---

Some caveats:

- Internal state is not preserved when content scrolls out of the render window. Make sure all your data is captured in the item data or external stores like Flux, Redux, or Relay.
- This is a `PureComponent` which means that it will not re-render if `props` are shallow-equal. Make sure that everything your `renderItem` function depends on is passed as a prop (e.g. `extraData`) that is not `===` after updates, otherwise your UI may not update on changes. This includes the `data` prop and parent component state.
- In order to constrain memory and enable smooth scrolling, content is rendered asynchronously offscreen. This means it's possible to scroll faster than the fill rate and momentarily see blank content. This is a tradeoff that can be adjusted to suit the needs of each application, and we are working on improving it behind the scenes.
- By default, the list looks for a `key` prop on each item and uses that for the React key. Alternatively, you can provide a custom `keyExtractor` prop.

---

# Reference

## Props

### [ScrollView Props](scrollview.md#props)

Inherits [ScrollView Props](scrollview.md#props).

---

### <div class="label required basic">Required</div> **`data`**

The default accessor functions assume this is an array of objects with shape `{key: string}` but you can override `getItem`, `getItemCount`, and `keyExtractor` to handle any type of index-based data.

| Type |
| ---- |
| any  |

---

### <div class="label required basic">Required</div> **`getItem`**

```jsx
(data: any, index: number) => object;
```

Um acessador genérico para extrair um item de qualquer tipo de blob de dados.

| Type     |
| -------- |
| function |

---

### <div class="label required basic">Required</div> **`getItemCount`**

```jsx
(data: any) => number;
```

Determina quantos itens estão no blob de dados.

| Type     |
| -------- |
| function |

---

### <div class="label required basic">Required</div> **`renderItem`**

```jsx
(info: any) => ?React.Element<any>
```

Pega um item de `dados` e o renderiza na lista

| Type     |
| -------- |
| function |

---

### `CellRendererComponent`

Cada célula é renderizada usando esse elemento. Pode ser uma classe de componente React ou uma função de renderização. O padrão é usar [`View`] (view.md).

| Type                |
| ------------------- |
| component, function |

---

### `ItemSeparatorComponent`

Renderizado entre cada item, mas não na parte superior ou inferior. Por padrão, os adereços `destacado` e `LeadingItem` são fornecidos. `renderItem` fornece `separators.highlight`/`unhighlight` que atualizará a prop `highlighted`, mas você também pode adicionar adereços personalizados com `separators.updateProps`.

| Type                |
| ------------------- |
| component, function |

---

### `ListEmptyComponent`

Renderizado quando a lista está vazia. Pode ser um Componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo, `<SomeComponent />`).

| Type               |
| ------------------ |
| component, element |

---

### `ListItemComponent`

Cada item de dados é renderizado usando esse elemento. Pode ser uma classe de componente React ou uma função de renderização.

| Type                |
| ------------------- |
| component, function |

---

### `ListFooterComponent`

Renderizado na parte inferior de todos os itens. Pode ser um Componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo, `<SomeComponent />`).

| Type               |
| ------------------ |
| component, element |

---

### `ListFooterComponentStyle`

Estilo para exibição interna para `ListFooterComponent`.

| Type          | Required |
| ------------- | -------- |
| ViewStyleProp | No       |

---

### `ListHeaderComponent`

Renderizado na parte superior de todos os itens. Pode ser um Componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo, `<SomeComponent />`).

| Type               |
| ------------------ |
| component, element |

---

### `ListHeaderComponentStyle`

Estilo para exibição interna para `ListHeaderComponent`.

| Type                           |
| ------------------------------ |
| [View Style](view-style-props) |

---

### `debug`

`debug` ativará o registro extra e as sobreposições visuais para ajudar na depuração do uso e da implementação, mas com um impacto significativo no desempenho.

| Type    |
| ------- |
| boolean |

---

### `disableVirtualization`

> **Descontinuado.** A virtualização fornece otimizações significativas de desempenho e memória, mas desmonta totalmente as instâncias react que estão fora da janela de renderização. Você só precisa desabilitar isso para fins de depuração.

| Type    |
| ------- |
| boolean |

---

### `extraData`

Uma propriedade de marcador para dizer à lista para renderizar novamente (já que implementa `PureComponent`). Se alguma das suas funções `renderItem`, Cabeçalho, Rodapé, etc. depender de qualquer coisa fora da prop `data`, cole-a aqui e trate-a imutavelmente.

| Type |
| ---- |
| any  |

---

### `getItemLayout`

```jsx
(
    data: any,
    index: number,
  ) => {length: number, offset: number, index: number}
```

| Type     |
| -------- |
| function |

---

### `horizontal`

Se `true`, renderiza itens próximos uns dos outros horizontalmente em vez de empilhados verticalmente.

| Type    |
| ------- |
| boolean |

---

### `initialNumToRender`

Quantos itens renderizar no lote inicial. Isso deve ser suficiente para preencher a tela, mas não muito mais. Observe que esses itens nunca serão desmontados como parte da renderização em janelas para melhorar o desempenho percebido das ações de rolagem para cima.

| Type   | Default |
| ------ | ------- |
| number | `10`    |

---

### `initialScrollIndex`

Em vez de começar no topo com o primeiro item, comece em `InitialScrolLindeX`. Isso desativa a otimização “rolar para o topo” que mantém os primeiros itens `InitialNumToRender` sempre renderizados e renderiza imediatamente os itens começando neste índice inicial. Requer `getItemLayout` para ser implementado.

| Type   |
| ------ |
| number |

---

### `inverted`

Inverte a direção da rolagem. Usa transformações de escala de `-1`.

| Type    |
| ------- |
| boolean |

---

### `listKey`

Um identificador exclusivo para esta lista. Se houver várias VirtualizedLists no mesmo nível de aninhamento em outra VirtualizedList, essa chave será necessária para que a virtualização funcione corretamente.

| Type   | Required |
| ------ | -------- |
| string | True     |

---

### `keyExtractor`

```jsx
(item: object, index: number) => string;
```

Usado para extrair uma chave exclusiva para um determinado item no índice especificado. A chave é usada para armazenamento em cache e como a chave react para rastrear a reordenação de itens. O extrator padrão verifica `item.key`, depois `item.id` e, em seguida, volta a usar o índice, como o React faz.

| Type     |
| -------- |
| function |

---

### `maxToRenderPerBatch`

O número máximo de itens a serem renderizados em cada lote de renderização incremental. Quanto mais renderizado de uma só vez, melhor será a taxa de preenchimento, mas a capacidade de resposta pode sofrer porque o conteúdo de renderização pode interferir na resposta a toques de botão ou outras interações.

| Type   |
| ------ |
| number |

---

### `onEndReached`

```jsx
(info: {distanceFromEnd: number}) => void
```

Chamado uma vez quando a posição de rolagem fica dentro de `onEndReachedThreshold` do conteúdo renderizado.

| Type     |
| -------- |
| function |

---

### `onEndReachedThreshold`

A que distância do final (em unidades de comprimento visível da lista) a borda inferior da lista deve estar do final do conteúdo para acionar o retorno de chamada `OnEndReached`. Assim, um valor de 0,5 acionará `OnEndReached` quando o final do conteúdo estiver dentro da metade do comprimento visível da lista.

| Type   |
| ------ |
| number |

---

### `onRefresh`

```jsx
() => void
```

Se fornecido, um `RefreshControl` padrão será adicionado para a funcionalidade “Puxar para atualizar”. Certifique-se também de definir a prop `refreshing` corretamente.

| Type     |
| -------- |
| function |

---

### `onScrollToIndexFailed`

```jsx
(info: {
    index: number,
    highestMeasuredFrameIndex: number,
    averageItemLength: number,
  }) => void
```

Usado para lidar com falhas ao rolar para um índice que ainda não foi medido. A ação recomendada é calcular seu próprio deslocamento e `ScrollTo`, ou rolar o mais longe possível e tentar novamente depois que mais itens forem renderizados.

| Type     |
| -------- |
| function |

---

### `onViewableItemsChanged`

Chamado quando a visibilidade das linhas muda, conforme definido pela prop `ViewabilityConfig`.

| Type                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------ |
| (callback: { changed: array of [ViewToken](viewtoken)s, viewableItems: array of [ViewToken](viewtoken)s }) => void |

---

### `persistentScrollbar`

| Type |
| ---- |
| bool |

---

### `progressViewOffset`

Defina isso quando o deslocamento for necessário para que o indicador de carregamento seja exibido corretamente.

| Type   |
| ------ |
| number |

---

### `refreshControl`

Um elemento de controle de atualização personalizado. Quando definido, ele substitui o componente padrão `<RefreshControl>` construído internamente. Os adereços OnRefresh e refrescantes também são ignorados. Funciona apenas para VirtualizedList vertical.

| Type    |
| ------- |
| element |

---

### `refreshing`

Defina isso como verdadeiro enquanto aguarda novos dados de uma atualização.

| Type    |
| ------- |
| boolean |

---

### `removeClippedSubviews`

Isso pode melhorar o desempenho de rolagem para listas grandes.

> Nota: Pode ter bugs (conteúdo ausente) em algumas circunstâncias - use por sua conta e risco.

| Type    |
| ------- |
| boolean |

---

### `renderScrollComponent`

```jsx
(props: object) => element;
```

Renderize um componente de rolagem personalizado, por exemplo, com um estilo diferente `RefreshControl`.

| Type     |
| -------- |
| function |

---

### `viewabilityConfig`

Consulte `ViewabilityHelper.js` para o tipo de fluxo e outras documentações.

| Type              |
| ----------------- |
| ViewabilityConfig |

---

### `viewabilityConfigCallbackPairs`

Lista de pares `ViewabilityConfig`/`OnViewableItemsChanged`. Um `OnViewableItemsChanged` específico será chamado quando as condições correspondentes do `ViewabilityConfig` forem atendidas. Consulte `ViewabilityHelper.js` para o tipo de fluxo e outras documentações.

| Type                                   |
| -------------------------------------- |
| array of ViewabilityConfigCallbackPair |

---

### `updateCellsBatchingPeriod`

Quantidade de tempo entre lotes de renderização de itens de baixo preço, por exemplo, para renderizar itens bastante fora da tela. Taxa de preenchimento/capacidade de resposta semelhante como `MaxToRenderPerBatch`.

| Type   |
| ------ |
| number |

---

### `windowSize`

Determina o número máximo de itens renderizados fora da área visível, em unidades de comprimentos visíveis. Portanto, se sua lista preencher a tela, `WindowSize= {21} `(o padrão) renderizará a área visível da tela mais até 10 telas acima e 10 abaixo da janela de exibição. Reduzir esse número reduzirá o consumo de memória e poderá melhorar o desempenho, mas aumentará a chance de que a rolagem rápida revele áreas em branco momentâneas de conteúdo não renderizado.

| Type   |
| ------ |
| number |

## Methods

### `flashScrollIndicators()`

```jsx
flashScrollIndicators();
```

---

### `getChildContext()`

```jsx
getChildContext () => Object;
```

O `Object` retornado consiste em:

- 'VirtualizedList' (Objeto). Este objeto consiste no seguinte:
  - GetScrollMetrics' (Função). Retorna um objeto com as seguintes propriedades: `{contentLength: number, Doffset: number, dt: number, offset: number, timestamp: number, velocity: number, visíbleLength: number}`.
  - 'horizontal' (booleano) - Opcional.
  - 'getOutermostParentListRef' (Function).
  - 'getNestedChildState' (Function) - Returns ChildListState .
  - 'RegisterAsNestedChild' (Função). Isso aceita um objeto com as seguintes propriedades `{CellKey: string, key: string, ref: VirtualizedList, ParentDebugInfo: ListDebugInfo}`. Ele retorna um ChildListState
  - 'UnregisterAsnestedChild' (Função). Isso pega um objeto com as seguintes propriedades, `{key: string, state: childListState}`
  - 'debugInfo' (ListDebugInfo).

---

### `getScrollableNode()`

```jsx
getScrollableNode () => ?number;
```

---

### `getScrollRef()`

```jsx
getScrollRef () => | ?React.ElementRef<typeof ScrollView>
    | ?React.ElementRef<typeof View>;
```

---

### `getScrollResponder()`

```jsx
getScrollResponder () => ?ScrollResponderType;
```

Fornece uma alça para o respondente de rolagem subjacente. Observe que `isso. _ScrollRef` pode não ser um `ScrollView`, então precisamos verificar se ele responde a `GetScrollResponder` antes de chamá-lo.

---

### `hasMore()`

```jsx
hasMore () => boolean;
```

---

### `scrollToEnd()`

```jsx
scrollToEnd((params: object));

Valid `params` consist of:

- 'animated' (boolean). Optional default is true.
```

---

### `scrollToIndex()`

```jsx
scrollToIndex((params: object));
```

`params` válidos consistem em:

- 'animado' (booleano). Opcional.
- 'índice' (número). Obrigatório.
- 'ViewOffset' (número). Opcional.
- 'ViewPosition' (número). Opcional.

---

### `scrollToItem()`

```jsx
scrollToItem((params: object));
```

`params` válidos consistem em:

- 'animado' (booleano). Opcional.
- 'item' (Item). Obrigatório.
- 'ViewPosition' (número). Opcional.

---

### `scrollToOffset()`

```jsx
scrollToOffset((params: object));
```

Role até um deslocamento de pixel de conteúdo específico na lista.

Param `offset` espera que o deslocamento role para. No caso de `horizontal` ser verdadeiro, o deslocamento é o valor x, em qualquer outro caso o deslocamento é o valor de Y.

Param `animated` (`true` por padrão) define se a lista deve fazer uma animação durante a rolagem.

---

### `recordInteraction()`

```jsx
recordInteraction();
```

---

### `setNativeProps()`

```jsx
setNativeProps((props: Object));
```
