---
id: shadow-props
title: Shadow Props
---

```SnackPlayer name=Shadow%20Props&supportedPlatforms=ios
import React, { useState } from "react";
import { Text, View, StyleSheet, Slider } from "react-native";

const ShadowPropSlider = ({ label, value, ...props }) => {
  return (
    <>
      <Text>
        {label} ({value.toFixed(2)})
      </Text>
      <Slider step={1} value={value} {...props} />
    </>
  );
}

const App = () => {
  const [shadowOffsetWidth, setShadowOffsetWidth] = useState(0);
  const [shadowOffsetHeight, setShadowOffsetHeight] = useState(0);
  const [shadowRadius, setShadowRadius] = useState(0);
  const [shadowOpacity, setShadowOpacity] = useState(0.1);

  return (
    <View style={styles.container}>
      <View
        style={[
          styles.square,
          {
            shadowOffset: {
              width: shadowOffsetWidth,
              height: -shadowOffsetHeight
            },
            shadowOpacity,
            shadowRadius
          }
        ]}
      />
      <View style={styles.controls}>
        <ShadowPropSlider
          label="shadowOffset - X"
          minimumValue={-50}
          maximumValue={50}
          value={shadowOffsetWidth}
          onValueChange={val => setShadowOffsetWidth(val)}
        />
        <ShadowPropSlider
          label="shadowOffset - Y"
          minimumValue={-50}
          maximumValue={50}
          value={shadowOffsetHeight}
          onValueChange={val => setShadowOffsetHeight(val)}
        />
        <ShadowPropSlider
          label="shadowRadius"
          minimumValue={0}
          maximumValue={100}
          value={shadowRadius}
          onValueChange={val => setShadowRadius(val)}
        />
        <ShadowPropSlider
          label="shadowOpacity"
          minimumValue={0}
          maximumValue={1}
          step={0.05}
          value={shadowOpacity}
          onValueChange={val => setShadowOpacity(val)}
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "space-around",
    backgroundColor: "#ecf0f1",
    padding: 8
  },
  square: {
    alignSelf: "center",
    backgroundColor: "white",
    borderRadius: 4,
    height: 150,
    shadowColor: "black",
    width: 150
  },
  controls: {
    paddingHorizontal: 12
  }
});

export default App;
```

# Reference

## Props

### `shadowColor`

Define a cor da sombra projetada.

Essa propriedade só funcionará na API 28 do Android ou superior. Para funcionalidades semelhantes em APIs Android inferiores, use a [`elevation` propriedade] (view-style-props #elevation).

| Type               |
| ------------------ |
| [color](colors.md) |

---

### `shadowOffset` <div class="label ios">iOS</div>

Sets the drop shadow offset.

| Type                                   |
| -------------------------------------- |
| object: {width: number,height: number} |

---

### `shadowOpacity` <div class="label ios">iOS</div>

Define a opacidade da sombra projetada (multiplicada pelo componente alfa da cor).

| Type   |
| ------ |
| number |

---

### `shadowRadius` <div class="label ios">iOS</div>

Define o raio de desfoque da sombra projetada.

| Type   |
| ------ |
| number |
