---
id: image-style-props
title: Image Style Props
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

## Examples

### Image Resize Mode

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Image%20Resize%20Modes%20Function%20Component%20Example
import React from "react";
import { View, Image, Text, StyleSheet } from "react-native";

const DisplayAnImageWithStyle = () => {
  return (
    <View style={styles.container}>
      <View>
        <Image
          style={{
            resizeMode: "cover",
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>resizeMode : cover</Text>
      </View>
      <View>
        <Image
          style={{
            resizeMode: "contain",
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>resizeMode : contain</Text>
      </View>
      <View>
        <Image
          style={{
            resizeMode: "stretch",
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>resizeMode : stretch</Text>
      </View>
      <View>
        <Image
          style={{
            resizeMode: "repeat",
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>resizeMode : repeat</Text>
      </View>
      <View>
        <Image
          style={{
            resizeMode: "center",
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>resizeMode : center</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "space-around",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Image%20Resize%20Modes%20Class%20Component%20Example
import React, { Component } from "react";
import { View, Image, StyleSheet, Text } from "react-native";

class DisplayAnImageWithStyle extends Component {
  render() {
    return (
      <View style={styles.container}>
        <View>
          <Image
            style={{
              resizeMode: "cover",
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>resizeMode : cover</Text>
        </View>
        <View>
          <Image
            style={{
              resizeMode: "contain",
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>resizeMode : contain</Text>
        </View>
        <View>
          <Image
            style={{
              resizeMode: "stretch",
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>resizeMode : stretch</Text>
        </View>
        <View>
          <Image
            style={{
              resizeMode: "repeat",
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>resizeMode : repeat</Text>
        </View>
        <View>
          <Image
            style={{
              resizeMode: "center",
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>resizeMode : center</Text>
        </View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "space-around",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
</Tabs>

### Image Border

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Style%20BorderWidth%20and%20BorderColor%20Function%20Component%20Example
import React from "react";
import { View, Image, StyleSheet, Text } from "react-native";

const DisplayAnImageWithStyle = () => {
  return (
    <View style={styles.container}>
      <Image
        style={{
          borderColor: "red",
          borderWidth: 5,
          height: 100,
          width: 200
        }}
        source={require("@expo/snack-static/react-native-logo.png")}
      />
      <Text>borderColor & borderWidth</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "center",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Style%20BorderWidth%20and%20BorderColor%20Class%20Component%20Example
import React, { Component } from "react";
import { View, Image, StyleSheet, Text } from "react-native";

class DisplayAnImageWithStyle extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Image
          style={{
            borderColor: "red",
            borderWidth: 5,
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>borderColor & borderWidth</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "center",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
</Tabs>

### Image Border Radius

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Style%20Border%20Radius%20Function%20Component%20Example
import React from "react";
import { View, Image, StyleSheet, Text } from "react-native";

const DisplayAnImageWithStyle = () => {
  return (
    <View style={styles.container}>
      <View>
        <Image
          style={{
            borderTopRightRadius: 20,
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>borderTopRightRadius</Text>
      </View>
      <View>
        <Image
          style={{
            borderBottomRightRadius: 20,
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>borderBottomRightRadius</Text>
      </View>
      <View>
        <Image
          style={{
            borderBottomLeftRadius: 20,
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>borderBottomLeftRadius</Text>
      </View>
      <View>
        <Image
          style={{
            borderTopLeftRadius: 20,
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>borderTopLeftRadius</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "space-around",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Style%20Border%20Radius%20Class%20Component%20Example
import React, { Component } from "react";
import { View, Image, StyleSheet, Text } from "react-native";

class DisplayAnImageWithStyle extends Component {
  render() {
    return (
      <View style={styles.container}>
        <View>
          <Image
            style={{
              borderTopRightRadius: 20,
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>borderTopRightRadius</Text>
        </View>
        <View>
          <Image
            style={{
              borderBottomRightRadius: 20,
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>borderBottomRightRadius</Text>
        </View>
        <View>
          <Image
            style={{
              borderBottomLeftRadius: 20,
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>borderBottomLeftRadius</Text>
        </View>
        <View>
          <Image
            style={{
              borderTopLeftRadius: 20,
              height: 100,
              width: 200
            }}
            source={require("@expo/snack-static/react-native-logo.png")}
          />
          <Text>borderTopLeftRadius</Text>
        </View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "space-around",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
</Tabs>

### Image Tint

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=Style%20tintColor%20Function%20Component
import React from "react";
import { View, Image, StyleSheet, Text } from "react-native";

const DisplayAnImageWithStyle = () => {
  return (
    <View style={styles.container}>
      <Image
        style={{
          tintColor: "#000000",
          resizeMode: "contain",
          height: 100,
          width: 200
        }}
        source={require("@expo/snack-static/react-native-logo.png")}
      />
      <Text>tintColor</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "center",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=Style%20tintColor%20Class%20Component
import React, { Component } from "react";
import { View, Image, StyleSheet, Text } from "react-native";

class DisplayAnImageWithStyle extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Image
          style={{
            tintColor: "#000000",
            resizeMode: "contain",
            height: 100,
            width: 200
          }}
          source={require("@expo/snack-static/react-native-logo.png")}
        />
        <Text>tintColor</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    display: "flex",
    flexDirection: "vertical",
    justifyContent: "center",
    alignItems: "center",
    height: "100%",
    textAlign: "center"
  }
});

export default DisplayAnImageWithStyle;
```

</TabItem>
</Tabs>

# Reference

## Props

### `backfaceVisibility`

A propriedade define se a face traseira de uma imagem girada deve ou não estar visível.

| Type                          | Default     |
| ----------------------------- | ----------- |
| enum(`'visible'`, `'hidden'`) | `'visible'` |

---

### `backgroundColor`

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `borderBottomLeftRadius`

| Type   |
| ------ |
| number |

---

### `borderBottomRightRadius`

| Type   |
| ------ |
| number |

---

### `borderColor`

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `borderRadius`

| Type   |
| ------ |
| number |

---

### `borderTopLeftRadius`

| Type   |
| ------ |
| number |

---

### `borderTopRightRadius`

| Type   |
| ------ |
| number |

---

### `borderWidth`

| Type   |
| ------ |
| number |

---

### `opacity`

Defina um valor de opacidade para a imagem. O número deve estar no intervalo de `0,0` a `1,0`.

| Type   | Default |
| ------ | ------- |
| number | `1.0`   |

---

### `overflow`

| Type                          | Default     |
| ----------------------------- | ----------- |
| enum(`'visible'`, `'hidden'`) | `'visible'` |

---

### `overlayColor` <div class="label android">Android</div>

Quando a imagem tiver cantos arredondados, especificar uma OverlayColor fará com que o espaço restante nos cantos seja preenchido com uma cor sólida. Isso é útil em casos que não são suportados pela implementação do Android de cantos arredondados:

- Certos modos de redimensionamento, como `'contain'`
- Animated GIFs

Uma maneira típica de usar essa prop é com imagens exibidas em um plano de fundo sólido e definir a `OverlayColor` para a mesma cor do plano de fundo.

Para obter detalhes sobre como isso funciona sob o capô, consulte [Documentação do Fresco] (https://frescolib.org/docs/rounded-corners-and-circles.html).

| Type   |
| ------ |
| string |

---

### `resizeMode`

| Type                                                              | Default   |
| ----------------------------------------------------------------- | --------- |
| enum(`'cover'`, `'contain'`, `'stretch'`, `'repeat'`, `'center'`) | `'cover'` |

---

### `tintColor`

Altera a cor de todos os pixels não transparentes para o TintColor.

| Type               |
| ------------------ |
| [color](colors.md) |
