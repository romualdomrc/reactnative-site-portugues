---
id: vibration
title: Vibration
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Vibra o dispositivo.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Vibration&supportedPlatforms=ios,android
import React from "react";
import { Button, Platform, Text, Vibration, View, SafeAreaView, StyleSheet } from "react-native";

const Separator = () => {
  return <View style={Platform.OS === "android" ? styles.separator : null} />;
}

const App = () => {

  const ONE_SECOND_IN_MS = 1000;

  const PATTERN = [
    1 * ONE_SECOND_IN_MS,
    2 * ONE_SECOND_IN_MS,
    3 * ONE_SECOND_IN_MS
  ];

  const PATTERN_DESC =
    Platform.OS === "android"
      ? "wait 1s, vibrate 2s, wait 3s"
      : "wait 1s, vibrate, wait 2s, vibrate, wait 3s";

  return (
    <SafeAreaView style={styles.container}>
      <Text style={[styles.header, styles.paragraph]}>Vibration API</Text>
      <View>
        <Button title="Vibrate once" onPress={() => Vibration.vibrate()} />
      </View>
      <Separator />
      {Platform.OS == "android"
        ? [
            <View>
              <Button
                title="Vibrate for 10 seconds"
                onPress={() => Vibration.vibrate(10 * ONE_SECOND_IN_MS)}
              />
            </View>,
            <Separator />
          ]
        : null}
      <Text style={styles.paragraph}>Pattern: {PATTERN_DESC}</Text>
      <Button
        title="Vibrate with pattern"
        onPress={() => Vibration.vibrate(PATTERN)}
      />
      <Separator />
      <Button
        title="Vibrate with pattern until cancelled"
        onPress={() => Vibration.vibrate(PATTERN, true)}
      />
      <Separator />
      <Button
        title="Stop vibration pattern"
        onPress={() => Vibration.cancel()}
        color="#FF0000"
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: 44,
    padding: 8
  },
  header: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  },
  paragraph: {
    margin: 24,
    textAlign: "center"
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Vibration&supportedPlatforms=ios,android
import React, { Component } from "react";
import { Button, Platform, Text, Vibration, View, SafeAreaView, StyleSheet } from "react-native";

const Separator = () => {
  return <View style={Platform.OS === "android" ? styles.separator : null} />;
}

class App extends Component {
  render() {
    const ONE_SECOND_IN_MS = 1000;

    const PATTERN = [
      1 * ONE_SECOND_IN_MS,
      2 * ONE_SECOND_IN_MS,
      3 * ONE_SECOND_IN_MS
    ];

    const PATTERN_DESC =
      Platform.OS === "android"
        ? "wait 1s, vibrate 2s, wait 3s"
        : "wait 1s, vibrate, wait 2s, vibrate, wait 3s";

    return (
      <SafeAreaView style={styles.container}>
        <Text style={[styles.header, styles.paragraph]}>Vibration API</Text>
        <View>
          <Button title="Vibrate once" onPress={() => Vibration.vibrate()} />
        </View>
        <Separator />
        {Platform.OS == "android"
          ? [
              <View>
                <Button
                  title="Vibrate for 10 seconds"
                  onPress={() => Vibration.vibrate(10 * ONE_SECOND_IN_MS)}
                />
              </View>,
              <Separator />
            ]
          : null}
        <Text style={styles.paragraph}>Pattern: {PATTERN_DESC}</Text>
        <Button
          title="Vibrate with pattern"
          onPress={() => Vibration.vibrate(PATTERN)}
        />
        <Separator />
        <Button
          title="Vibrate with pattern until cancelled"
          onPress={() => Vibration.vibrate(PATTERN, true)}
        />
        <Separator />
        <Button
          title="Stop vibration pattern"
          onPress={() => Vibration.cancel()}
          color="#FF0000"
        />
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: 44,
    padding: 8
  },
  header: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  },
  paragraph: {
    margin: 24,
    textAlign: "center"
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth
  }
});

export default App;
```

</TabItem>
</Tabs>

> Os aplicativos Android devem solicitar a permiss??o `android.permission.vibrate` adicionando `<uses-permission android:name="android.permission.VIBRATE"/>` a `AndroidManifest.xml`.

> A API Vibration ?? implementada como uma chamada `AudioServicesPlaySystemSound (KSystemSoundid_Vibrate) `no iOS.

---

# Refer??ncia

## M??todos

### `cancel()`

```jsx
Vibration.cancel();
```

Chame isso para parar de vibrar depois de ter invocado `vibrate () `com a repeti????o ativada.

---

### `vibrate()`

```jsx
Vibration.vibrate(pattern, repeat);
```

Aciona uma vibra????o com dura????o fixa.

**No Android, ** a dura????o da vibra????o ?? padr??o de 400 milissegundos, e uma dura????o de vibra????o arbitr??ria pode ser especificada passando um n??mero como o valor para o argumento `padr??o`. **No iOS, ** a dura????o da vibra????o ?? fixada em cerca de 400 milissegundos.

O m??todo `vibrate () `pode receber um argumento `padr??o` com uma matriz de n??meros que representam o tempo em milissegundos. Voc?? pode definir `repeit` como true para percorrer o padr??o de vibra????o em um loop at?? que `cancel () `seja chamado.

**No Android, ** os ??ndices ??mpares da matriz `padr??o` representam a dura????o da vibra????o, enquanto os pares representam o tempo de separa????o. **No iOS, ** os n??meros na matriz `padr??o` representam o tempo de separa????o, pois a dura????o da vibra????o ?? fixa.

**Par??metros: **

| Nome    | Tipo                                                                     | Padr??o | Descri????o                                                                                       |
| ------- | ------------------------------------------------------------------------ | ------- | ------------------------------------------------------------------------------------------------- |
| pattern | number <div className="label android">Android</div><hr/>array of numbers | `400`   | Dura????o da vibra????o em milissegundos. <hr/> Padr??o de vibra????o como uma matriz de n??meros em milissegundos. |
| repeat  | boolean                                                                  | `false` | Repita o padr??o de vibra????o at?? `cancel () `.                                                        |
