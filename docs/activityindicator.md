---
id: activityindicator
title: ActivityIndicator
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Exibe um indicador circular de carregamento.

## Examplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=ActivityIndicator%20Function%20Component%20Example
import React from "react";
import { ActivityIndicator, StyleSheet, Text, View } from "react-native";

const App = () => (
  <View style={[styles.container, styles.horizontal]}>
    <ActivityIndicator />
    <ActivityIndicator size="large" />
    <ActivityIndicator size="small" color="#0000ff" />
    <ActivityIndicator size="large" color="#00ff00" />
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center"
  },
  horizontal: {
    flexDirection: "row",
    justifyContent: "space-around",
    padding: 10
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=ActivityIndicator%20Class%20Component%20Example
import React, { Component } from "react";
import { ActivityIndicator, StyleSheet, Text, View } from "react-native";

class App extends Component {
  render() {
    return (
      <View style={[styles.container, styles.horizontal]}>
        <ActivityIndicator />
        <ActivityIndicator size="large" />
        <ActivityIndicator size="small" color="#0000ff" />
        <ActivityIndicator size="large" color="#00ff00" />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center"
  },
  horizontal: {
    flexDirection: "row",
    justifyContent: "space-around",
    padding: 10
  }
});

export default App;
```

</TabItem>
</Tabs>

# Referencia

## Props

### [View Props](view#props)

Herda de [View Props](view#props).

---

### `animating`

Mostra o indicador (`true`) ou esconde (`false`).

TIPO | PADRÃO
-----|-------
bool | `true`

---

### `color`

A cor do indicador.

| TIPO            | PADRÃO                                                                                                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [color](colors) | `null` (system accent default color)<div class="label android">Android</div><hr/><ins style={{background: '#999'}} className="color-box" />`'#999999'` <div className="label ios">iOS</div> |

---

### `hidesWhenStopped` <div class="label ios">iOS</div>

Oculta o indicador se não estiver animado.

| Type | Default |
| ---- | ------- |
| bool | `true`  |

---

### `size`

Tamanho do indicador.

| Type                                                                           | Default   |
| ------------------------------------------------------------------------------ | --------- |
| enum(`'small'`, `'large'`)<hr/>number <div class="label android">Android</div> | `'small'` |
