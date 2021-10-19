---
id: button
title: Button
---

# Button
Um componente básico de botão que deve renderizar de boas em qualquer plataforma. Suporta uma quantidade mínima de customização.

Se o botão não ficar legal no seu app, você pode construir o seu próprio botão usando o TouchableOpacity ou o TouchableWithoutFeedback. Para se inspirar, dê uma olhadinha no [código fonte do componente de botão](https://github.com/facebook/react-native/blob/master/Libraries/Components/Button.js) ou nos [botões criados pela comunidade](https://js.coach/?menu%5Bcollections%5D=React%20Native&page=1&query=button).

```tsx
<Button
  onPress={onPressLearnMore}
  title="Learn More"
  color="#841584"
  accessibilityLabel="Learn more about this purple button"
/>
```

## Exemplo

```SnackPlayer name=Button%20Example
import React from 'react';
import { StyleSheet, Button, View, SafeAreaView, Text, Alert } from 'react-native';

const Separator = () => (
  <View style={styles.separator} />
);

const App = () => (
  <SafeAreaView style={styles.container}>
    <View>
      <Text style={styles.title}>
        The title and onPress handler are Obrigatório. It is recommended to set accessibilityLabel to help make your app usable by everyone.
      </Text>
      <Button
        title="Press me"
        onPress={() => Alert.alert('Simple Button pressed')}
      />
    </View>
    <Separator />
    <View>
      <Text style={styles.title}>
        Adjust the color in a way that looks standard on each platform. On  iOS, the color prop controls the color of the text. On Android, the color adjusts the background color of the button.
      </Text>
      <Button
        title="Press me"
        color="#f194ff"
        onPress={() => Alert.alert('Button with adjusted color pressed')}
      />
    </View>
    <Separator />
    <View>
      <Text style={styles.title}>
        All interaction for the component are disabled.
      </Text>
      <Button
        title="Press me"
        disabled
        onPress={() => Alert.alert('Cannot press this one')}
      />
    </View>
    <Separator />
    <View>
      <Text style={styles.title}>
        This layout strategy lets the title define the width of the button.
      </Text>
      <View style={styles.fixToText}>
        <Button
          title="Left button"
          onPress={() => Alert.alert('Left button pressed')}
        />
        <Button
          title="Right button"
          onPress={() => Alert.alert('Right button pressed')}
        />
      </View>
    </View>
  </SafeAreaView>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    marginHorizontal: 16,
  },
  title: {
    textAlign: 'center',
    marginVertical: 8,
  },
  fixToText: {
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: '#737373',
    borderBottomWidth: StyleSheet.hairlineWidth,
  },
});

export default App;
```

---

# Referência

## Propriedades

### <div class="label Obrigatório basic">Obrigatório</div>**`onPress`**

Handler que é chamado quando o usuário aperta no botão.

| Type                               |
| ---------------------------------- |
| function([PressEvent](pressevent)) |

---

### <div class="label Obrigatório basic">Obrigatório</div>**`title`**

Texto que vai aparecer dentro do botão. No Android o texto vai ser convertido pra caixa alta.

| Type   |
| ------ |
| string |

---

### `accessibilityLabel`

Text to display for blindness accessibility features.

| Type   |
| ------ |
| string |

---

### `color`

Cor do texto no iOS ou do fundo do botão no Android.

| Type            | Default                                                                                                                                                                                                                                   |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [color](colors) | <ins style={{background: '#2196F3'}} className="color-box" /> `'#2196F3'` <div className="label android">Android</div><hr/><ins style={{background: '#007AFF'}} className="color-box" /> `'#007AFF'` <div className="label ios">iOS</div> |

---

### `disabled`

Se `true`, desabilita todas as interações desse componente.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `hasTVPreferredFocus` <div class="label tv">TV</div>

Isso aqui eu acho que é pra ver se tem foco preferido em TVs.

| Type | Default |
| ---- | ------- |
| bool | `false` |

---

### `nextFocusDown` <div class="label android">Android</div><div class="label tv">TV</div>

Escolhe a próxima view a receber o foco quando o usuário navegar para baixo. [Veja a documentação do Android.](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusDown).

| Type   |
| ------ |
| number |

---

### `nextFocusForward` <div class="label android">Android</div><div class="label tv">TV</div>

Escolhe a próxima view a receber o foco quando o usuário navegar para frente. [Veja a documentação do Android.](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusForward).

| Type   |
| ------ |
| number |

---

### `nextFocusLeft` <div class="label android">Android</div><div class="label tv">TV</div>

Escolhe a próxima view a receber o foco quando o usuário navegar para a esquerda. [Veja a documentação do Android.](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusLeft).

| Type   |
| ------ |
| number |

---

### `nextFocusRight` <div class="label android">Android</div><div class="label tv">TV</div>

Escolhe a próxima view a receber o foco quando o usuário navegar para a direita. [Veja a documentação do Android.](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusRight).

| Type   |
| ------ |
| number |

---

### `nextFocusUp` <div class="label android">Android</div><div class="label tv">TV</div>

Escolhe a próxima view a receber o foco quando o usuário navegar para cima. [Veja a documentação do Android.](https://developer.android.com/reference/android/view/View.html#attr_android:nextFocusUp).

| Type   |
| ------ |
| number |

---

### `testID`

Usado pra localizar esta view em testes de ponta-a-ponta.

| Type   |
| ------ |
| string |

---

### `touchSoundDisabled` <div class="label android">Android</div>

Se `true`, não toca o som do sistema quando aperta o botão.

| Type    | Default |
| ------- | ------- |
| boolean | `false` |
