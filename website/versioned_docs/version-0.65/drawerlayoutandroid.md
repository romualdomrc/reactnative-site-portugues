---
id: drawerlayoutandroid
title: DrawerLayoutAndroid
---

Componente React que envolve a plataforma `DrawerLayout` (somente Android). A gaveta (normalmente usada para navegação) é renderizada com `RenderNavigationView` e os filhos diretos são a exibição principal (para onde vai seu conteúdo). A visualização de navegação inicialmente não é visível na tela, mas pode ser puxada do lado da janela especificada pela propriedade `DrawerPosition` e sua largura pode ser definida pela propriedade `DrawerWidth`.

## Exemplo

```SnackPlayer name=DrawerLayoutAndroid%20Component%20Example&supportedPlatforms=android
import React, { useRef, useState } from "react";
import { Button, DrawerLayoutAndroid, Text, StyleSheet, View } from "react-native";

const App = () => {
  const drawer = useRef(null);
  const [drawerPosition, setDrawerPosition] = useState("left");
  const changeDrawerPosition = () => {
    if (drawerPosition === "left") {
      setDrawerPosition("right");
    } else {
      setDrawerPosition("left");
    }
  };

  const navigationView = () => (
    <View style={[styles.container, styles.navigationContainer]}>
      <Text style={styles.paragraph}>I'm in the Drawer!</Text>
      <Button
        title="Close drawer"
        onPress={() => drawer.current.closeDrawer()}
      />
    </View>
  );

  return (
    <DrawerLayoutAndroid
      ref={drawer}
      drawerWidth={300}
      drawerPosition={drawerPosition}
      renderNavigationView={navigationView}
    >
      <View style={styles.container}>
        <Text style={styles.paragraph}>
          Drawer on the {drawerPosition}!
        </Text>
        <Button
          title="Change Drawer Position"
          onPress={() => changeDrawerPosition()}
        />
        <Text style={styles.paragraph}>
          Swipe from the side or press button below to see it!
        </Text>
        <Button
          title="Open drawer"
          onPress={() => drawer.current.openDrawer()}
        />
      </View>
    </DrawerLayoutAndroid>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    padding: 16
  },
  navigationContainer: {
    backgroundColor: "#ecf0f1"
  },
  paragraph: {
    padding: 16,
    fontSize: 15,
    textAlign: "center"
  }
});

export default App;
```

---

# Reference

## Props

### [View Props](view.md#props)

Inherits [View Props](view.md#props).

---

### `drawerBackgroundColor`

Specifies the background color of the drawer. The default value is `white`. If you want to set the opacity of the drawer, use rgba. Example:

```jsx
return (
  <DrawerLayoutAndroid drawerBackgroundColor="rgba(0,0,0,0.5)" />
);
```

| Tipo               | Obrigatório |
| ------------------ | -------- |
| [color](colors.md) | No       |

---

### `drawerLockMode`

Especifica o modo de bloqueio da gaveta. A gaveta pode ser trancada em 3 estados:

- desbloqueado (padrão), o que significa que a gaveta responderá (abrir/fechar) aos gestos de toque.
- trancado fechado, o que significa que a gaveta permanecerá fechada e não responderá aos gestos.
- trancado aberto, o que significa que a gaveta permanecerá aberta e não responderá aos gestos. A gaveta ainda pode ser aberta e fechada programaticamente (`OpenDrawer`/`Closedrawer`).

| Tipo                                             | Obrigatório |
| ------------------------------------------------ | -------- |
| enum('unlocked', 'locked-closed', 'locked-open') | No       |

---

### `drawerPosition`

Especifica o lado da tela a partir do qual a gaveta deslizará. Por padrão, ele está definido como `esquerda`.

| Tipo                  | Obrigatório |
| --------------------- | -------- |
| enum('left', 'right') | No       |

---

### `drawerWidth`

Especifica a largura da gaveta, mais precisamente a largura da vista que será puxada da borda da janela.

| Tipo   | Obrigatório |
| ------ | -------- |
| number | No       |

---

### `keyboardDismissMode`

Determina se o teclado é descartado em resposta a um arrasto.

- 'nenhum' (o padrão), os arrastos não descartam o teclado.
- 'on-drag', o teclado é descartado quando um arrasto começa.

| Tipo                    | Obrigatório |
| ----------------------- | -------- |
| enum('none', 'on-drag') | No       |

---

### `onDrawerClose`

Função chamada sempre que a visualização de navegação for fechada.

| Tipo     | Obrigatório |
| -------- | -------- |
| function | No       |

---

### `onDrawerOpen`

Função chamada sempre que a visualização de navegação for aberta.

| Tipo     | Obrigatório |
| -------- | -------- |
| function | No       |

---

### `onDrawerSlide`

Função chamada sempre que houver uma interação com a visualização de navegação.

| Tipo     | Obrigatório |
| -------- | -------- |
| function | No       |

---

### `onDrawerStateChanged`

Função chamada quando o estado da gaveta mudou. A gaveta pode estar em 3 estados:

- ocioso, o que significa que não há interação com a visualização de navegação acontecendo no momento
- arrastando, o que significa que há atualmente uma interação com a visualização de navegação
- assentamento, o que significa que houve uma interação com a visualização de navegação, e a visualização de navegação agora está terminando sua animação de fechamento ou abertura

| Tipo     | Obrigatório |
| -------- | -------- |
| function | No       |

---

### `renderNavigationView`

A visualização de navegação que será renderizada ao lado da tela e pode ser puxada.

| Tipo     | Obrigatório |
| -------- | -------- |
| function | Yes      |

---

### `statusBarBackgroundColor`

Faça com que a gaveta pegue a tela inteira e desenhe o plano de fundo da barra de status para permitir que ela abra sobre a barra de status. Isso só terá efeito na API 21+.

| Tipo               | Obrigatório |
| ------------------ | -------- |
| [color](colors.md) | No       |

## Métodos

### `closeDrawer()`

```jsx
closeDrawer();
```

Fecha a gaveta.

---

### `openDrawer()`

```jsx
openDrawer();
```

Abre a gaveta.
