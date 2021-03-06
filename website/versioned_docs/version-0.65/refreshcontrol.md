---
id: refreshcontrol
title: RefreshControl
---

Este componente é usado dentro de um ScrollView ou ListView para adicionar pull para atualizar a funcionalidade. Quando o ScrollView está em `scrollY: 0`, swiping down triggers andeslizar para baixo aciona um evento `onRefresh`.

## Example

```SnackPlayer name=RefreshControl&supportedPlatforms=ios,android
import React from 'react';
import { RefreshControl, SafeAreaView, ScrollView, StyleSheet, Text } from 'react-native';

const wait = (timeout) => {
  return new Promise(resolve => setTimeout(resolve, timeout));
}

const App = () => {
  const [refreshing, setRefreshing] = React.useState(false);

  const onRefresh = React.useCallback(() => {
    setRefreshing(true);
    wait(2000).then(() => setRefreshing(false));
  }, []);

  return (
    <SafeAreaView style={styles.container}>
      <ScrollView
        contentContainerStyle={styles.scrollView}
        refreshControl={
          <RefreshControl
            refreshing={refreshing}
            onRefresh={onRefresh}
          />
        }
      >
        <Text>Pull down to see RefreshControl indicator</Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  scrollView: {
    flex: 1,
    backgroundColor: 'pink',
    alignItems: 'center',
    justifyContent: 'center',
  },
});

export default App;
```

> Nota: `refreshing` é um prop controlado, é por isso que precisa ser definido como` true` na função `onRefresh`, caso contrário o indicador de atualização irá parar imediatamente.

---

# Reference

## Props

### [View Props](view.md#props)

Inherits [View Props](view.md#props).

---

### <div class="label required basic">Required</div>**`refreshing`**

Se a visualização deve indicar uma atualização ativa.

| Type    |
| ------- |
| boolean |

---

### `colors` <div class="label android">Android</div>

As cores (pelo menos uma) que serão usadas para desenhar o indicador de atualização.

| Type                         |
| ---------------------------- |
| array of [colors](colors.md) |

---

### `enabled` <div class="label android">Android</div>

Se a funcionalidade puxar para atualizar está habilitada.

| Type    | Default |
| ------- | ------- |
| boolean | `true`  |

---

### `onRefresh`

Chamado quando a visualização começa a ser atualizada.

| Type     |
| -------- |
| function |

---

### `progressBackgroundColor` <div class="label android">Android</div>

A cor de fundo do indicador de atualização.

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `progressViewOffset`

Deslocamento superior da vista de progresso.

| Type   | Default |
| ------ | ------- |
| number | `0`     |

---

### `size` <div class="label android">Android</div>

Tamanho do indicador de atualização.

| Type                                                             | Default                          |
| ---------------------------------------------------------------- | -------------------------------- |
| [RefreshControl.SIZE](refreshcontrol.md#refreshlayoutconstssize) | RefreshLayoutConsts.SIZE.DEFAULT |

---

### `tintColor` <div class="label ios">iOS</div>

A cor do indicador de atualização.

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `title` <div class="label ios">iOS</div>

O título exibido sob o indicador de atualização.

| Type   |
| ------ |
| string |

---

### `titleColor` <div class="label ios">iOS</div>

A cor do título do indicador de atualização.

| Type               |
| ------------------ |
| [color](colors.md) |

## Type Definitions

### RefreshLayoutConsts.SIZE

As constantes do componente Android SwipeRefreshLayout. O tamanho real do componente pode variar entre os dispositivos. Você pode ler mais sobre o componente nativo na documentação [Android documentation](https://developer.android.com/reference/androidx/swiperefreshlayout/widget/SwipeRefreshLayout).

| Type |
| ---- |
| enum |

**Constants:**

| Name    | Type | Value | Description                 |
| ------- | ---- | ----- | --------------------------- |
| DEFAULT | int  | `1`   | Default RefreshControl size |
| LARGE   | int  | `0`   | Large RefreshControl size   |
