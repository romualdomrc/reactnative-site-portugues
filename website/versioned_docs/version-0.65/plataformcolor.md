---
id: platformcolor
title: PlatformColor
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

```js
PlatformColor(color1, [color2, ...colorN]);
```

Você pode usar a função `PlatformColor` para acessar cores nativas na plataforma de destino, fornecendo o valor da string correspondente da cor nativa. Você passa uma string para a função `PlatformColor` e, desde que ela exista nessa plataforma, ela retornará a cor nativa correspondente, que você pode aplicar em qualquer parte do seu aplicativo.

Se você passar mais de um valor de string para a função `PlatformColor`, ele tratará o primeiro valor como padrão e o restante como fallback.

```js
PlatformColor('bogusName', 'linkColor');
```

Como as cores nativas podem ser sensíveis a temas e/ou alto contraste, essa lógica específica da plataforma também se traduz dentro de seus componentes.

### Cores compatíveis

Para obter uma lista completa dos tipos de cores do sistema compatíveis, consulte:

- Android:
  - [R.attr](https://developer.android.com/reference/android/R.attr) - `?attr` prefix
  - [R.color](https://developer.android.com/reference/android/R.color) - `@android:color` prefix
- iOS (Objective-C and Swift notations):
  - [UIColor Standard Colors](https://developer.apple.com/documentation/uikit/uicolor/standard_colors)
  - [UIColor UI Element Colors](https://developer.apple.com/documentation/uikit/uicolor/ui_element_colors)

#### Notas do desenvolvedor

<Tabs groupId="guide" defaultValue="web" values={constants.getDevNotesTabs(["web"])}>

<TabItem value="web">

> Se você está familiarizado com sistemas de design, outra maneira de pensar sobre isso é que o `PlatformColor` permite que você aproveite os tokens de cores do sistema de design local para que seu aplicativo possa se misturar perfeitamente!

</TabItem>
</Tabs>

## Exemplo

```SnackPlayer name=PlatformColor%20Example&supportedPlatforms=android,ios
import React from 'react';
import {
  Platform,
  PlatformColor,
  StyleSheet,
  Text,
  View
} from 'react-native';

const App = () => (
  <View style={styles.container}>
    <Text style={styles.label}>
      I am a special label color!
    </Text>
  </View>
);

const styles = StyleSheet.create({
  label: {
    padding: 16,
    ...Platform.select({
      ios: {
        color: PlatformColor('label'),
        backgroundColor:
          PlatformColor('systemTealColor'),
      },
      android: {
        color: PlatformColor('?android:attr/textColor'),
        backgroundColor:
          PlatformColor('@android:color/holo_blue_bright'),
      },
      default: { color: 'black' }
    })
  },
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  }
});

export default App;
```

O valor da string fornecido para a função `PlatformColor` deve corresponder à string como ela existe na plataforma nativa em que o aplicativo está sendo executado. Para evitar erros de tempo de execução, a função deve ser encapsulada em uma verificação de plataforma, seja através de um `platform.os === 'platform'` ou um `platform.select () `, como mostrado no exemplo acima.

> **Nota: ** Você pode encontrar um exemplo completo que demonstra o uso adequado e pretendido de `PlatformColor` em [PlatformColorExample.js] (https://github.com/facebook/react-native/blob/master/packages/rn-tester/js/examples/PlatformColor/PlatformColorExample.js).
