---
id: transforms
title: Transforms
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

Transformações são propriedades de estilo que ajudarão você a modificar a aparência e a posição de seus componentes usando transformações 2D ou 3D. No entanto, depois de aplicar transformações, os layouts permanecem os mesmos em torno do componente transformado, portanto, ele pode se sobrepor aos componentes próximos. Você pode aplicar margem ao componente transformado, aos componentes próximos ou ao preenchimento ao contêiner para evitar tais sobreposições.

## Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Transforms
import React from "react";
import { SafeAreaView, ScrollView, StyleSheet, Text, View } from "react-native";

const App = () => (
  <SafeAreaView style={styles.container}>
    <ScrollView
      contentContainerStyle={styles.scrollContentContainer}
    >
      <View style={styles.box}>
        <Text style={styles.text}>Original Object</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ scale: 2 }]
      }]}>
        <Text style={styles.text}>Scale by 2</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ scaleX: 2 }]
      }]}>
        <Text style={styles.text}>ScaleX by 2</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ scaleY: 2 }]
      }]}>
        <Text style={styles.text}>ScaleY by 2</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ rotate: "45deg" }]
      }]}>
        <Text style={styles.text}>Rotate by 45 deg</Text>
      </View>

      <View style={[styles.box, {
        transform: [
          { rotateX: "45deg" },
          { rotateZ: "45deg" }
        ]
      }]}>
        <Text style={styles.text}>Rotate X&Z by 45 deg</Text>
      </View>

      <View style={[styles.box, {
        transform: [
          { rotateY: "45deg" },
          { rotateZ: "45deg" }
        ]
      }]}>
        <Text style={styles.text}>Rotate Y&Z by 45 deg</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ skewX: "45deg" }]
      }]}>
        <Text style={styles.text}>SkewX by 45 deg</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ skewY: "45deg" }]
      }]}>
        <Text style={styles.text}>SkewY by 45 deg</Text>
      </View>

      <View style={[styles.box, {
        transform: [
          { skewX: "30deg" },
          { skewY: "30deg" }
        ]
      }]}>
        <Text style={styles.text}>Skew X&Y by 30 deg</Text>
      </View>

      <View style={[styles.box, {
        transform: [{ translateX: -50 }]
      }]}>
        <Text style={styles.text}>TranslateX by -50 </Text>
      </View>

      <View style={[styles.box, {
        transform: [{ translateY: 50 }]
      }]}>
        <Text style={styles.text}>TranslateY by 50 </Text>
      </View>
    </ScrollView>
  </SafeAreaView>
);

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  scrollContentContainer: {
    alignItems: "center",
    paddingBottom: 60
  },
  box: {
    height: 100,
    width: 100,
    borderRadius: 5,
    marginVertical: 40,
    backgroundColor: "#61dafb",
    alignItems: "center",
    justifyContent: "center"
  },
  text: {
    fontSize: 14,
    fontWeight: "bold",
    margin: 8,
    color: "#000",
    textAlign: "center"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Transforms
import React, { Component } from "react";
import { SafeAreaView, ScrollView, StyleSheet, Text, View } from "react-native";

class App extends Component {
  render() {
    return (
      <SafeAreaView style={styles.container}>
        <ScrollView
          contentContainerStyle={styles.scrollContentContainer}
        >
          <View style={styles.box}>
            <Text style={styles.text}>Original Object</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ scale: 2 }]
          }]}>
            <Text style={styles.text}>Scale by 2</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ scaleX: 2 }]
          }]}>
            <Text style={styles.text}>ScaleX by 2</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ scaleY: 2 }]
          }]}>
            <Text style={styles.text}>ScaleY by 2</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ rotate: "45deg" }]
          }]}>
            <Text style={styles.text}>Rotate by 45 deg</Text>
          </View>

          <View style={[styles.box, {
            transform: [
              { rotateX: "45deg" },
              { rotateZ: "45deg" }
            ]
          }]}>
            <Text style={styles.text}>Rotate X&Z by 45 deg</Text>
          </View>

          <View style={[styles.box, {
            transform: [
              { rotateY: "45deg" },
              { rotateZ: "45deg" }
            ]
          }]}>
            <Text style={styles.text}>Rotate Y&Z by 45 deg</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ skewX: "45deg" }]
          }]}>
            <Text style={styles.text}>SkewX by 45 deg</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ skewY: "45deg" }]
          }]}>
            <Text style={styles.text}>SkewY by 45 deg</Text>
          </View>

          <View style={[styles.box, {
            transform: [
              { skewX: "30deg" },
              { skewY: "30deg" }
            ]
          }]}>
            <Text style={styles.text}>Skew X&Y by 30 deg</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ translateX: -50 }]
          }]}>
            <Text style={styles.text}>TranslateX by -50</Text>
          </View>

          <View style={[styles.box, {
            transform: [{ translateY: 50 }]
          }]}>
            <Text style={styles.text}>TranslateY by 50</Text>
          </View>
        </ScrollView>
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  scrollContentContainer: {
    alignItems: "center",
    paddingBottom: 60
  },
  box: {
    height: 100,
    width: 100,
    borderRadius: 5,
    marginVertical: 40,
    backgroundColor: "#61dafb",
    alignItems: "center",
    justifyContent: "center"
  },
  text: {
    fontSize: 14,
    fontWeight: "bold",
    margin: 8,
    color: "#000",
    textAlign: "center"
  }
});

export default App;
```

</TabItem>
</Tabs>

---

# Referência

## Métodos

### `transform()`

`transform` aceita uma matriz de objetos de transformação. Cada objeto especifica a propriedade que será transformada como a chave e o valor a ser usado na transformação. Os objetos não devem ser combinados. Use um único par chave/valor por objeto.

As transformações de rotação requerem uma string para que a transformação possa ser expressa em graus (deg) ou radianos (rad). Por exemplo:

```js
transform([{ rotateX: '45deg' }, { rotateZ: '0.785398rad' }]);
```

As transformações distorcidas requerem uma string para que a transformação possa ser expressa em graus (deg). Por exemplo:

```js
transform([{ skewX: '45deg' }]);
```

| Tipo                                                                                                                                                                                                                                                                      | Obrigatório |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| array of objects: {matrix: number[]}, {perspective: number}, {rotate: string}, {rotateX: string}, {rotateY: string}, {rotateZ: string}, {scale: number}, {scaleX: number}, {scaleY: number}, {translateX: number}, {translateY: number}, {skewX: string}, {skewY: string} | No       |

---

### `decomposedMatrix`, `rotation`, `scaleX`, `scaleY`, `transformMatrix`, `translateX`, `translateY`

> **Descontinuado.** Use a prop [`transform`] (transforma #transform) em vez disso.
