---
id: sectionlist
title: SectionList
---

importar guias de '@ theme / Tabs'; importar TabItem de '@ theme / TabItem'; importar constantes de '@ site / core / TabsConstants';

Uma interface de alto desempenho para renderizar listas seccionadas, suportando os recursos mais úteis:

- Totalmente multiplataforma.
- Callbacks de visibilidade configuráveis.
- Suporte ao cabeçalho da lista.
- Suporte de rodapé de lista.
- Suporte para separador de itens.
- Suporte ao cabeçalho da seção.
- Suporte do separador de seção.
- Suporte de renderização de dados e itens heterogêneos.
- Puxe para atualizar.
- Carregamento de rolagem.

Se você não precisa de suporte de seção e deseja uma interface mais simples, use [`<FlatList>`] (flatlist.md). 

## Example

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=SectionList%20Example
import React from "react";
import { StyleSheet, Text, View, SafeAreaView, SectionList, StatusBar } from "react-native";

const DATA = [
  {
    title: "Main dishes",
    data: ["Pizza", "Burger", "Risotto"]
  },
  {
    title: "Sides",
    data: ["French Fries", "Onion Rings", "Fried Shrimps"]
  },
  {
    title: "Drinks",
    data: ["Water", "Coke", "Beer"]
  },
  {
    title: "Desserts",
    data: ["Cheese Cake", "Ice Cream"]
  }
];

const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);

const App = () => (
  <SafeAreaView style={styles.container}>
    <SectionList
      sections={DATA}
      keyExtractor={(item, index) => item + index}
      renderItem={({ item }) => <Item title={item} />}
      renderSectionHeader={({ section: { title } }) => (
        <Text style={styles.header}>{title}</Text>
      )}
    />
  </SafeAreaView>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
    marginHorizontal: 16
  },
  item: {
    backgroundColor: "#f9c2ff",
    padding: 20,
    marginVertical: 8
  },
  header: {
    fontSize: 32,
    backgroundColor: "#fff"
  },
  title: {
    fontSize: 24
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=SectionList%20Example
import React, { Component } from "react";
import { StyleSheet, Text, View, SafeAreaView, SectionList, StatusBar } from "react-native";

const DATA = [
  {
    title: "Main dishes",
    data: ["Pizza", "Burger", "Risotto"]
  },
  {
    title: "Sides",
    data: ["French Fries", "Onion Rings", "Fried Shrimps"]
  },
  {
    title: "Drinks",
    data: ["Water", "Coke", "Beer"]
  },
  {
    title: "Desserts",
    data: ["Cheese Cake", "Ice Cream"]
  }
];

const Item = ({ title }) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);

class App extends Component {
  render() {
    return (
      <SafeAreaView style={styles.container}>
        <SectionList
          sections={DATA}
          keyExtractor={(item, index) => item + index}
          renderItem={({ item }) => <Item title={item} />}
          renderSectionHeader={({ section: { title } }) => (
            <Text style={styles.header}>{title}</Text>
          )}
        />
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
    marginHorizontal: 16
  },
  item: {
    backgroundColor: "#f9c2ff",
    padding: 20,
    marginVertical: 8
  },
  header: {
    fontSize: 32,
    backgroundColor: "#fff"
  },
  title: {
    fontSize: 24
  }
});

export default App;
```

</TabItem>
</Tabs>

Este é um wrapper de conveniência em torno de [`<VirtualizedList>`] (virtualizedlist.md) e, portanto, herda seus props (bem como aqueles de [`<ScrollView>`] (scrollview.md)) que não estão explicitamente listados aqui , junto com as seguintes advertências:

- O estado interno não é preservado quando o conteúdo rola para fora da janela de renderização. Certifique-se de que todos os seus dados sejam capturados nos dados do item ou armazenamentos externos como Flux, Redux ou Relay.
- Este é um `PureComponent`, o que significa que não será renderizado novamente se` props` permanecer raso igual. Certifique-se de que tudo de que sua função `renderItem` depende seja passado como um prop (por exemplo,` extraData`) que não é `===` após as atualizações, caso contrário, sua IU pode não ser atualizada nas mudanças. Isso inclui a propriedade `data` e o estado do componente pai.
- Para restringir a memória e permitir a rolagem suave, o conteúdo é renderizado de forma assíncrona fora da tela. Isso significa que é possível rolar mais rápido do que a taxa de preenchimento e ver momentaneamente o conteúdo em branco. Essa é uma troca que pode ser ajustada para atender às necessidades de cada aplicativo e estamos trabalhando para melhorá-la nos bastidores.
- Por padrão, a lista procura por uma propriedade `chave` em cada item e a usa para a chave React. Alternativamente, você pode fornecer uma prop `keyExtractor` personalizada.

---

# Referência

## Props

### [ScrollView Props] (scrollview.md # props)

Herda [ScrollView Props] (scrollview.md # props).

---

### <div class = "label required basic"> Obrigatório </div> ** `renderItem` **

Representante padrão para cada item em cada seção. Pode ser anulado em uma base por seção. Deve retornar um elemento React.

| Tipo |
| -------- |
| função |

A função de renderização receberá um objeto com as seguintes chaves:

- 'item' (objeto) - o objeto do item conforme especificado na chave `data` desta seção
- 'índice' (número) - Índice do item dentro da seção.
- 'seção' (objeto) - O objeto de seção completa conforme especificado em `seções`.
- 'separadores' (objeto) - Um objeto com as seguintes chaves:
  - 'destaque' (função) - `() => void`
  - 'unhighlight' (função) - `() => void`
  - 'updateProps' (função) - `(selecionar, newProps) => void`
    - 'select' (enum) - os valores possíveis são 'inicial', 'final'
    - 'newProps' (objeto) 

---

### <div class="label required basic">Required</div>**`sections`**

Os dados reais a serem renderizados, semelhantes ao prop `data` em [` FlatList`] (flatlist.md). 

| Type                                        |
| ------------------------------------------- |
| array of [Section](sectionlist.md#section)s |

---

### `extraData`

Uma propriedade de marcador para informar a lista para renderizar novamente (uma vez que implementa `PureComponent`). Se qualquer uma de suas funções `renderItem`, Header, Footer, etc. depender de qualquer coisa fora do prop` data`, coloque-o aqui e trate-o de forma imutável.

| Tipo |
| ---- |
| qualquer |

---

### `initialNumToRender`

Quantos itens renderizar no lote inicial. Isso deve ser suficiente para preencher a tela, mas não muito mais. Observe que esses itens nunca serão desmontados como parte da renderização em janela para melhorar o desempenho percebido das ações de rolar para cima.

| Tipo | Padrão |
| ------ | ------- |
| número | `10` |

---

### `invertido`

Inverte a direção da rolagem. Usa transformações de escala de -1.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

---

### `ItemSeparatorComponent`

Renderizado entre cada item, mas não na parte superior ou inferior. Por padrão, os adereços `realçados`,` seção` e `[à esquerda / à direita] [Item / Seção]` são fornecidos. `renderItem` fornece` separators.highlight` / `unhighlight` que irá atualizar o prop` realçado`, mas você também pode adicionar props personalizados com `separators.updateProps`.

| Tipo |
| ------------------ |
| componente, elemento |

---

### `keyExtractor`

Usado para extrair uma chave exclusiva para um determinado item no índice especificado. A chave é usada para armazenamento em cache e como a chave React para rastrear o reordenamento de itens. O extrator padrão verifica `item.key` e, em seguida, volta a usar o índice, como o React faz. Observe que isso define chaves para cada item, mas cada seção geral ainda precisa de sua própria chave.

| Tipo |
| --------------------------------------- |
| (item: objeto, índice: número) => string |

---

### `ListEmptyComponent`

Renderizado quando a lista está vazia. Pode ser um componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo,` <SomeComponent /> `).

| Tipo |
| ------------------ |
| componente, elemento |

---

### `ListFooterComponent`

Renderizado no final da lista. Pode ser um componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo,` <SomeComponent /> `).

| Tipo |
| ------------------ |
| componente, elemento |

---

### `ListHeaderComponent`

Renderizado no início da lista. Pode ser um componente React (por exemplo, `SomeComponent`) ou um elemento React (por exemplo,` <SomeComponent /> `).

| Tipo |
| ------------------ |
| componente, elemento |

---

### `onEndReached`

Chamado uma vez quando a posição de rolagem fica dentro de `onEndReachedThreshold` do conteúdo renderizado.

| Tipo |
| ------------------------------------------- |
| (info: {distanceFromEnd: number}) => void |

---

### `onEndReachedThreshold`

A que distância do final (em unidades de comprimento visível da lista) a borda inferior da lista deve estar do final do conteúdo para acionar o retorno de chamada `onEndReached`. Assim, um valor de 0,5 irá disparar `onEndReached` quando o final do conteúdo estiver na metade do comprimento visível da lista. 

| Type   | Default |
| ------ | ------- |
| number | `2`     |

---

### `onRefresh`

Se fornecido, um RefreshControl padrão será adicionado para a funcionalidade "Pull to Refresh". Certifique-se também de definir o prop `refreshing` corretamente. Para deslocar o RefreshControl do topo (por exemplo, em 100 pontos), use `progressViewOffset = {100}`.

| Tipo |
| -------- |
| função |

---

### `onViewableItemsChanged`

Chamado quando a visibilidade das linhas muda, conforme definido pela propriedade `viewabilityConfig`.

| Tipo |
| -------------------------------------------------- -------------------------------------------------- -------------- |
| (retorno de chamada: {alterado: matriz de [ViewToken] (viewtoken) s, viewableItems: matriz de [ViewToken] (viewtoken) s}) => void |

---

### `refreshing`

Defina isso como verdadeiro enquanto espera por novos dados de uma atualização.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

---

### `removeClippedSubviews`

> Nota: pode haver bugs (conteúdo ausente) em algumas circunstâncias - use por sua própria conta e risco.

Isso pode melhorar o desempenho de rolagem para listas grandes.

| Tipo | Padrão |
| ------- | ------- |
| booleano | `false` |

---

### `renderSectionFooter`

Renderizado na parte inferior de cada seção.

| Tipo |
| -------------------------------------------------- -------------------- |
| (info: {section: [Section] (sectionlist # section)}) => elemento, `null` |

---

### `renderSectionHeader`

Renderizado no topo de cada seção. Eles ficam na parte superior do `ScrollView` por padrão no iOS. Veja `stickySectionHeadersEnabled`.

| Tipo |
| -------------------------------------------------- -------------------- |
| (info: {section: [Section] (sectionlist # section)}) => elemento, `null` |

---

### `SectionSeparatorComponent`

Renderizado nas partes superior e inferior de cada seção (observe que isso é diferente de `ItemSeparatorComponent`, que só é renderizado entre itens). Eles têm como objetivo separar as seções dos cabeçalhos acima e abaixo e normalmente têm a mesma resposta de realce que `ItemSeparatorComponent`. Também recebe `realçado`,` [à esquerda / à direita] [Item / Seção] `, e quaisquer adereços personalizados de` separators.updateProps`.

| Tipo |
| ------------------ |
| componente, elemento |

---

### `stickySectionHeadersEnabled`

Faz com que os cabeçalhos de seção fiquem presos na parte superior da tela até que o próximo o empurre. Só habilitado por padrão no iOS porque esse é o padrão da plataforma lá.

| Tipo | Padrão |
| ------- | -------------------------------------------------- ---------------------------------------------- |
| booleano | `false` <div class =" label android "> Android </div> <hr />` true` <div className = "label ios"> iOS </div> |

## Métodos

### `flashScrollIndicators ()` <div class = "label ios"> iOS </div>

`` `jsx
flashScrollIndicators ();
`` `

Exibe os indicadores de rolagem momentaneamente.

---

### `recordInteraction ()`

`` `jsx
recordInteraction ();
`` `

Informa à lista que ocorreu uma interação, o que deve acionar cálculos de visibilidade, por exemplo, se `waitForInteractions` for verdadeiro e o usuário não tiver rolado. Isso normalmente é chamado por toques em itens ou por ações de navegação. 

---

### `scrollToLocation()`

```jsx
scrollToLocation(params);
```

Rola até o item no `sectionIndex` e` itemIndex` especificados (dentro da seção) posicionado na área visível de modo que `viewPosition` 0 o coloque no topo (e pode ser coberto por um cabeçalho aderente), 1 no final e 0,5 centralizado no meio.

> Nota: Não é possível rolar para locais fora da janela de renderização sem especificar a propriedade `getItemLayout` ou` onScrollToIndexFailed`.

** Parâmetros: **

| Nome Tipo |
| -------------------------------------------------- ----- | ------ |
| params <div class = "label basic required"> Obrigatório </div> | objeto |

As chaves `params` válidas são:

- 'animado' (booleano) - Se a lista deve fazer uma animação durante a rolagem. O padrão é `true`.
- 'itemIndex' (número) - Índice dentro da seção para o item a ser rolado. Obrigatório.
- 'sectionIndex' (número) - Índice da seção que contém o item para o qual rolar. Obrigatório.
- 'viewOffset' (número) - Um número fixo de pixels para compensar a posição de destino final, por exemplo, para compensar cabeçalhos fixos.
- 'viewPosition' (número) - Um valor de `0` coloca o item especificado pelo índice no topo,` 1` na parte inferior e `0,5` centralizado no meio.

## Definições de tipo

### Seção

Um objeto que identifica os dados a serem renderizados para uma determinada seção.

| Tipo |
| ---- |
| qualquer |

** Propriedades: **

| Nome Tipo | Descrição
| -------------------------------------------------- --- | ------------------ | -------------------------------------------------- -------------------------------------------------- -------------------------------------------------- ------------- |
| data <div class = "label basic required"> Obrigatório </div> | matriz | Os dados para renderizar itens nesta seção. Array de objetos, muito parecido com a [propriedade de dados de `FlatList`] (flatlist # data). |
| chave | string | Tecla opcional para controlar o reordenamento da seção. Se você não planeja reordenar as seções, o índice do array será usado por padrão. |
| renderItem | função | Opcionalmente, defina um representante de item arbitrário para esta seção, sobrescrevendo o [`renderItem`] padrão (sectionlist # renderitem) para a lista. |
| ItemSeparatorComponent | componente, elemento | Opcionalmente, defina um separador de item arbitrário para esta seção, substituindo o padrão [`ItemSeparatorComponent`] (sectionlist # itemseparatorcomponent) para a lista. |
| keyExtractor | função | Opcionalmente, defina um extrator de chave arbitrário para esta seção, substituindo o padrão [`keyExtractor`] (lista de seção # keyextractor). | 
