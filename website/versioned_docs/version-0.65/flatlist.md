---
id: flatlist
title: FlatList
---

Uma interface de alto desempenho para renderizar listas simples básicas, suportando os recursos mais úteis:

- Totalmente multiplataforma.
- Modo horizontal opcional.
- Retornos de chamada de visibilidade configuráveis.
- Suporte de cabeçalho.
- Suporte de rodapé.
- Suporte de separador.
- Puxe para atualizar.
- Carregamento de rolagem.
- Suporte a ScrollToIndex.
- Suporte a várias colunas.

Se você precisar de suporte de seção, use [`<SectionList>`] (sectionlist.md).

## Exemplo

```SnackPlayer name=flatlist-simple
import React from 'react';
import { SafeAreaView, View, FlatList, StyleSheet, Text, StatusBar } from 'react-native';

const DATA = [
  {
    id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb28ba',
    title: 'First Item',
  },
  {
    id: '3ac68afc-c605-48d3-a4f8-fbd91aa97f63',
    title: 'Second Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Third Item',
  },
];

const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);

const App = () => {
  const renderItem = ({ item }) => (
    <Item title={item.title} />
  );

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={item => item.id}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight || 0,
  },
  item: {
    backgroundColor: '#f9c2ff',
    padding: 20,
    marginVertical: 8,
    marginHorizontal: 16,
  },
  title: {
    fontSize: 32,
  },
});

export default App;
```

Para renderizar várias colunas, use a propriedade [`NumColumns`] (flatlist.md #numcolumns). Usar essa abordagem em vez de um layout `FlexWrap` pode evitar conflitos com a lógica de altura do item.

Exemplo mais complexo e selecionável abaixo.

- Ao passar `ExtraData= {selectEid} `para `FlatList`, garantimos que o próprio `FlatList` será renderizado novamente quando o estado mudar. Sem configurar essa prop, `FlatList` não saberia que precisa renderizar novamente quaisquer itens porque é um `PureComponent` e a comparação de prop não mostrará nenhuma alteração.
- `KeyExtractor` diz à lista para usar os `id`s para as chaves react em vez da propriedade `key` padrão.

```Snackplayer name=flatlist-selecionável
importar React, {useState} de “react”;
import {FlatList, SafeAreaView, StatusBar, StyleSheet, Texto, TouchableOpacity} de “react-native”;

const DATA = [
 {
 id: “bd7acbea-c1b1-46c2-aed5-3ad53abb28ba”,
 title: “Primeiro Item”,
 },
 {
 id: “3ac68afc-c605-48d3-a4f8-fbd91aa97f63",
 title: “Segundo Item”,
 },
 {
 id: “58694a0f-3da1-471f-bd96-145571e29d72",
 title: “Terceiro Item”,
 },
];

const Item = ({item, onPress, BackgroundColor, TextColor}) => (
 <TouchableOpacity onPress={onPress} style={[styles.item, backgroundColor]}> 
 <Text style={[styles.title, textColor]}> {item.title} </Text> 
 </TouchableOpacity> 
);

const App = () => {
 const [selectIDd, setSelecteId] = useState (nulo);

 const renderItem = ({item}) => {
 const BackgroundColor = item.id === Selecionado? “#6e3b6e": "#f9c2ff “;
 const color = item.id === SelecionadEid? 'branco': 'preto';

 retorno (
 <Item
 item= {item}
 onPress= {() => definir ID selecionado (item.id)}
 Cor de fundo = {{BackgroundColor}}
 TextColor= {{color}}
 />
 );
 };

 retorno (
 <SafeAreaView style={styles.container}> 
 <Lista plana
 dados= {DATA}
 RenderItem= {renderItem}
 KeyExtractor = {(item) => item.id}
 ExtraData= {selectEid}
 />
 </SafeAreaView> 
 );
};

const styles = StyleSheet.create ({
 recipiente: {
 flex: 1,
 MarginTop: Barra de status. altura atual || 0,
 },
 item: {
 preenchimento: 20,
 Margem vertical: 8,
 Margem horizontal: 16,
 },
 title: {
 Tamanho da fonte: 32,
 },
});

exportar aplicativo padrão;
```

Este é um invólucro de conveniência em torno de [`<VirtualizedList>`] (virtualizedlist.md) e, portanto, herda seus adereços (bem como os de [`<ScrollView>`] (scrollview.md)) que não estão explicitamente listados aqui, juntamente com as seguintes advertências:

- O estado interno não é preservado quando o conteúdo sai da janela de renderização. Certifique-se de que todos os seus dados sejam capturados nos dados do item ou em lojas externas, como Flux, Redux ou Relay.
- Este é um `PureComponent`, o que significa que ele não será renderizado novamente se `props` permanecerem rasos iguais. Certifique-se de que tudo o que sua função `RenderItem` depende é passado como uma prop (por exemplo, `ExtraData`) que não é `===` após as atualizações, caso contrário, sua IU pode não atualizar as alterações. Isso inclui a propriedade `data` e o estado do componente pai.
- Para restringir a memória e permitir a rolagem suave, o conteúdo é renderizado de forma assíncrona fora da tela. Isso significa que é possível rolar mais rápido do que a taxa de preenchimento e ver momentaneamente o conteúdo em branco. Essa é uma compensação que pode ser ajustada para atender às necessidades de cada aplicativo, e estamos trabalhando para melhorá-la nos bastidores.
- Por padrão, a lista procura uma prop `key` em cada item e a usa para a chave React. Como alternativa, você pode fornecer uma propriedade `KeyExtractor` personalizada.

---

# Referência

## Props

### [ScrollView Props](scrollview.md#props)

Herda [ScrollView Props] (scrollview.md #props), a menos que esteja aninhado em outra FlatList da mesma orientação.

---

### <div class="label required basic">Required</div> **`renderItem`**

```jsx
renderItem({ item, index, separators });
```

Pega um item de `dados` e o renderiza na lista.

Fornece metadados adicionais como `index` se você precisar, bem como uma função `separators.updateProps` mais genérica que permite definir quaisquer adereços que você deseja alterar a renderização do separador principal ou do separador à direita no caso do `highlight` e `unhighlight` mais comuns (que definem o` destaque: prop boolean`) são insuficientes para o seu caso de uso.

| Type     |
| -------- |
| function |

- `item` (Objeto): O item de `dados` sendo renderizado.
- `index` (número): O índice correspondente a este item na matriz `data`.
- `separators` (Object)
  - `highlight` (Function)
  - `unhighlight` (Function)
  - `updateProps` (Function)
    - `select` (enum('leading', 'trailing'))
    - `newProps` (Object)

Exemplo de uso:

```jsx
<FlatList
  ItemSeparatorComponent={
    Platform.OS !== 'android' &&
    (({ highlighted }) => (
      <View
        style={[
          style.separator,
          highlighted && { marginLeft: 0 }
        ]}
      />
    ))
  }
  data={[{ title: 'Title Text', key: 'item1' }]}
  renderItem={({ item, index, separators }) => (
    <TouchableHighlight
      key={item.key}
      onPress={() => this._onPress(item)}
      onShowUnderlay={separators.highlight}
      onHideUnderlay={separators.unhighlight}>
      <View style={{ backgroundColor: 'white' }}>
        <Text>{item.title}</Text>
      </View>
    </TouchableHighlight>
  )}
/>
```

---

### <div class="label required basic">Required</div> **`data`**

Para simplificar, os dados são uma matriz simples. Se você quiser usar outra coisa, como uma lista imutável, use o subjacente [`VirtualizedList`] (virtualizedlist.md) diretamente.

| Type  |
| ----- |
| array |

---

### `ItemSeparatorComponent`

Renderizado entre cada item, mas não na parte superior ou inferior. Por padrão, os adereços `destacado` e `LeadingItem` são fornecidos. `renderItem` fornece `separators.highlight`/`unhighlight` que atualizará a prop `highlighted`, mas você também pode adicionar adereços personalizados com `separators.updateProps`.

| Type      |
| --------- |
| component |

---

### `ListEmptyComponent`

Renderizado quando a lista está vazia. Pode ser um Componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo, `<SomeComponent />`).

| Type               |
| ------------------ |
| component, element |

---

### `ListFooterComponent`

Renderizado na parte inferior de todos os itens. Pode ser um Componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo, `<SomeComponent />`).

| Type               |
| ------------------ |
| component, element |

---

### `ListFooterComponentStyle`

Estilo para exibição interna para `ListFooterComponent`.

| Type                           |
| ------------------------------ |
| [View Style](view-style-props) |

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

### `columnWrapperStyle`

Estilo personalizado opcional para linhas de vários itens geradas quando `NumColumns > 1`.

| Type                           |
| ------------------------------ |
| [View Style](view-style-props) |

---

### `extraData`

Uma propriedade de marcador para dizer à lista para renderizar novamente (já que implementa `PureComponent`). Se alguma das suas funções `renderItem`, Cabeçalho, Rodapé, etc. depender de qualquer coisa fora da prop `data`, cole-a aqui e trate-a imutavelmente.

| Type |
| ---- |
| any  |

---

### `getItemLayout`

```jsx
(data, index) => {length: number, offset: number, index: number}
```

`GetItemLayout` é uma otimização opcional que permite pular a medição de conteúdo dinâmico se você souber o tamanho (altura ou largura) dos itens antes do tempo. `GetItemLayout` é eficiente se você tiver itens de tamanho fixo, por exemplo:

```jsx
  getItemLayout={(data, index) => (
    {length: ITEM_HEIGHT, offset: ITEM_HEIGHT * index, index}
  )}
```

Adicionar `GetItemLayout` pode ser um grande aumento de desempenho para listas de várias centenas de itens. Lembre-se de incluir o comprimento do separador (altura ou largura) no cálculo do deslocamento se você especificar `ItemSeparatorComponent`.

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

### `keyExtractor`

```jsx
(item: object, index: number) => string;
```

Usado para extrair uma chave exclusiva para um determinado item no índice especificado. A chave é usada para armazenamento em cache e como a chave react para rastrear a reordenação de itens. O extrator padrão verifica `item.key`, depois `item.id` e, em seguida, volta a usar o índice, como o React faz.

| Type     |
| -------- |
| function |

---

### `numColumns`

Várias colunas só podem ser renderizadas com `horizontal= {false} `e zig-zag como um layout `FlexWrap`. Os itens devem ter a mesma altura - layouts de alvenaria não são suportados.

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

Se fornecido, um RefreshControl padrão será adicionado para a funcionalidade “Puxar para atualizar”. Certifique-se também de definir a prop `refreshing` corretamente.

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

### `progressViewOffset`

Defina isso quando o deslocamento for necessário para que o indicador de carregamento seja exibido corretamente.

| Type   |
| ------ |
| number |

---

### `refreshing`

Defina isso como verdadeiro enquanto aguarda novos dados de uma atualização.

| Type    |
| ------- |
| boolean |

---

### `removeClippedSubviews`

Isso pode melhorar o desempenho de rolagem para listas grandes. No Android, o valor padrão é `true`.

> Nota: Pode ter bugs (conteúdo ausente) em algumas circunstâncias - use por sua conta e risco.

| Type    |
| ------- |
| boolean |

---

### `viewabilityConfig`

Consulte [`ViewabilityHelper.js`] (https://github.com/facebook/react-native/blob/master/Libraries/Lists/ViewabilityHelper.js) para o tipo de fluxo e documentação adicional.

| Type              |
| ----------------- |
| ViewabilityConfig |

`ViewabilityConfig` usa um tipo `ViewAbilityConfig` um objeto com as seguintes propriedades

| Property                         | Type    |
| -------------------------------- | ------- |
| minimumViewTime                  | number  |
| viewAreaCoveragePercentThreshold | number  |
| itemVisiblePercentThreshold      | number  |
| waitForInteraction               | boolean |

Pelo menos um dos `ViewareaCoveragePercentThreshold` ou `ItemVisiblePercentThreshold` é necessário. Isso precisa ser feito no `construtor` para evitar o seguinte erro ([ref] (https://github.com/facebook/react-native/issues/17408)):

```
 Erro: Não há suporte para alterar ViewabilityConfig em tempo real
```

```jsx
constructor (props) {
  super(props)

  this.viewabilityConfig = {
      waitForInteraction: true,
      viewAreaCoveragePercentThreshold: 95
  }
}
```

```jsx
<FlatList
    viewabilityConfig={this.viewabilityConfig}
  ...
```

#### minimumViewTime

Tempo mínimo (em milissegundos) em que um item deve ser fisicamente visível antes que o retorno de chamada de visibilidade seja acionado. Um número alto significa que percorrer o conteúdo sem parar não marcará o conteúdo como visível.

#### viewAreaCoveragePercentThreshold

Porcentagem da viewport que deve ser coberta para um item parcialmente ocluído contabilizar como “visível”, 0-100. Itens totalmente visíveis são sempre considerados visíveis. Um valor de 0 significa que um único pixel na janela de exibição torna o item visível, e um valor de 100 significa que um item deve estar totalmente visível ou cobrir toda a janela de visualização para contar como visível.

#### itemVisiblePercentThreshold

Semelhante a `ViewareACoveragePercentThreshold`, mas considera a porcentagem do item visível, em vez da fração da área visível que ele cobre.

#### waitForInteraction

Nada é considerado visível até que o usuário role ou `RecordInteraction` seja chamado após a renderização.

---

### `viewabilityConfigCallbackPairs`

Lista de pares `ViewabilityConfig`/`OnViewableItemsChanged`. Um `OnViewableItemsChanged` específico será chamado quando as condições correspondentes do `ViewabilityConfig` forem atendidas. Consulte `ViewabilityHelper.js` para o tipo de fluxo e outras documentações.

| Type                                   |
| -------------------------------------- |
| array de viewabilityConfigCallbackPair |

## Métodos

### `flashScrollIndicators()`

```jsx
flashScrollIndicators();
```

Exibe os indicadores de rolagem momentaneamente.

---

### `getNativeScrollRef()`

```jsx
getNativeScrollRef();
```

Fornece uma referência ao componente de rolagem subjacente

---

### `getScrollResponder()`

```jsx
getScrollResponder();
```

Fornece uma alça para o respondente de rolagem subjacente.

---

### `getScrollableNode()`

```jsx
getScrollableNode();
```

Fornece um identificador para o nó de rolagem subjacente.

---

### `recordInteraction()`

```jsx
recordInteraction();
```

Informa à lista que uma interação ocorreu, o que deve acionar cálculos de visibilidade, por exemplo, se `WaitForInteractions` for verdadeiro e o usuário não tiver rolado. Isso geralmente é chamado por toques em itens ou por ações de navegação.

---

### `scrollToEnd()`

```jsx
scrollToEnd(params);
```

Rola até o final do conteúdo. Pode ser instável sem o prop `getItemLayout`.

**Parâmetros: **

| Name   | Type   |
| ------ | ------ |
| params | object |

Chaves `params` válidas são:

- 'animated' (booleano) - Se a lista deve fazer uma animação durante a rolagem. O padrão é `true`.

---

### `scrollToIndex()`

```jsx
scrollToIndex(params);
```

Rola para o item no índice especificado de forma que ele seja posicionado na área visível de modo que `ViewPosition` 0 o coloque na parte superior, 1 na parte inferior e 0,5 centralizado no meio.

> Nota: Não é possível rolar para locais fora da janela de renderização sem especificar a propriedade `getItemLayout`.

**Parâmetros: **

| Name                                                        | Type   |
| ----------------------------------------------------------- | ------ |
| params <div className="label basic required">Required</div> | object |

Chaves `params` válidas são:

- 'animated' (booleano) - Se a lista deve fazer uma animação durante a rolagem. O padrão é `true`.
- 'index' (número) - O índice para rolar. Obrigatório.
- 'ViewOffset' (número) - Um número fixo de pixels para deslocar a posição final do alvo.
- 'ViewPosition' (número) - Um valor de `0` coloca o item especificado por índice na parte superior, `1` na parte inferior e `0,5` centralizado no meio.

---

### `scrollToItem()`

```jsx
scrollToItem(params);
```

Requer varredura linear através de dados - use `ScrollToIndex` em vez disso, se possível.

> Nota: Não é possível rolar para locais fora da janela de renderização sem especificar a propriedade `getItemLayout`.

**Parâmetros: **

| Name                                                        | Type   |
| ----------------------------------------------------------- | ------ |
| params <div className="label basic required">Required</div> | object |

Valid `params` keys are:

- 'animated' (booleano) - Se a lista deve fazer uma animação durante a rolagem. O padrão é `true`.
- 'item' (objeto) - O item para o qual rolar. Obrigatório.
- 'viewPosition' (number)

---

### `scrollToOffset()`

```jsx
scrollToOffset(params);
```

Role até um deslocamento de pixel de conteúdo específico na lista.

**Parâmetros: **

| Name                                                        | Type   |
| ----------------------------------------------------------- | ------ |
| params <div className="label basic required">Required</div> | object |

Chaves `params` válidas são:

- 'offset' (número) - O deslocamento para rolar. No caso de `horizontal` ser verdadeiro, o deslocamento é o valor x, em qualquer outro caso o deslocamento é o valor de Y. Obrigatório.
- 'animated' (booleano) - Se a lista deve fazer uma animação durante a rolagem. O padrão é `true`.
