---
id: animatedvaluexy
title: Animated.ValueXY
---

Valor 2D para gerar animações 2D, como gestos de panorâmica. API quase idêntica à normal [`Animated.Value`] (animatedvalue), mas multiplexada. Contém dois `Animated.Value`s regulares sob o capô.

## Exemplo

```SnackPlayer name=Animated.ValueXY
import React, { useRef } from "react";
import { Animated, PanResponder, StyleSheet, View } from "react-native";

const DraggableView = () => {
  const pan = useRef(new Animated.ValueXY()).current;

  const panResponder = PanResponder.create({
    onStartShouldSetPanResponder: () => true,
    onPanResponderMove: Animated.event([
      null,
      {
        dx: pan.x, // x,y are Animated.Value
        dy: pan.y,
      },
    ]),
    onPanResponderRelease: () => {
      Animated.spring(
        pan, // Auto-multiplexed
        { toValue: { x: 0, y: 0 } } // Back to zero
      ).start();
    },
  });

  return (
    <View style={styles.container}>
      <Animated.View
        {...panResponder.panHandlers}
        style={[pan.getLayout(), styles.box]}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  box: {
    backgroundColor: "#61dafb",
    width: 80,
    height: 80,
    borderRadius: 4,
  },
});

export default DraggableView;
```

---

# Reference

## Methods

### `setValue()`

```jsx
setValue(value);
```

Defina diretamente o valor. Isso interromperá todas as animações em execução no valor e atualizará todas as propriedades vinculadas.

**Parâmetros: **

| Nome  | Tipo   | Obrigatório | Descrição |
| ----- | ------ | -------- | ----------- |
| value | number | sim      | Valor       |

---

### `setOffset()`

```jsx
setOffset(offset);
```

Define um deslocamento que é aplicado sobre qualquer valor definido, seja via `setValue`, uma animação ou `Animated.event`. Útil para compensar coisas como o início de um gesto de pan.

**Parâmetros: **

| Nome   | Tipo   | Obrigatório | Descrição  |
| ------ | ------ | -------- | ------------ |
| offset | number | sim      | Valor de deslocamento |

---

### `flattenOffset()`

```jsx
flattenOffset();
```

Mescla o valor do deslocamento com o valor base e redefine o deslocamento para zero. A saída final do valor permanece inalterada.

---

### `extractOffset()`

```jsx
extractOffset();
```

Define o valor de deslocamento para o valor base e redefine o valor base para zero. A saída final do valor permanece inalterada.

---

### `addListener()`

```jsx
addListener(callback);
```

Adiciona um ouvinte assíncrono ao valor para que você possa observar atualizações de animações. Isso é útil porque não há como ler o valor de forma síncrona, pois ele pode ser direcionado nativamente.

Retorna uma string que serve como um identificador para o ouvinte.

**Parâmetros: **

| Nome     | Tipo     | Obrigatório | Descrição                                                                                 |
| -------- | -------- | -------- | ------------------------------------------------------------------------------------------- |
| callback | function | sim      | A função de retorno de chamada que receberá um objeto com uma chave `valor` definida para o novo valor. |

---

### `removeListener()`

```jsx
removeListener(id);
```

Cancele o registro de um ouvinte. O parâmetro `id` deve corresponder ao identificador retornado anteriormente por `addListener () `.

**Parâmetros: **

| Nome | Tipo   | Obrigatório | Descrição                        |
| ---- | ------ | -------- | ---------------------------------- |
| id   | string | sim      | Id do ouvinte que está sendo removido. |

---

### `removeAllListeners()`

```jsx
removeAllListeners();
```

Remova todos os ouvintes registrados.

---

### `stopAnimation()`

```jsx
stopAnimation([callback]);
```

Interrompe qualquer animação ou rastreamento em execução. `callback` é invocado com o valor final após a interrupção da animação, o que é útil para atualizar o estado para corresponder à posição da animação com o layout.

**Parâmetros: **

| Nome     | Tipo     | Obrigatório | Descrição                                   |
| -------- | -------- | -------- | --------------------------------------------- |
| callback | function | Não       | Uma função que receberá o valor final. |

---

### `resetAnimation()`

```jsx
resetAnimation([callback]);
```

Interrompe qualquer animação e redefine o valor para o original.

**Parâmetros: **

| Nome     | Tipo     | Obrigatório | Descrição                                      |
| -------- | -------- | -------- | ------------------------------------------------ |
| callback | function | Não       | Uma função que receberá o valor original. |

---

### `getLayout()`

```jsx
getLayout();
```

Converte `{x, y}` em `{left, top}` para uso em estilo, por exemplo.

```jsx
style={this.state.anim.getLayout()}
```

---

### `getTranslateTransform()`

```jsx
getTranslateTransform();
```

Converte `{x, y}` em uma transformação de tradução utilizável, por exemplo.

```jsx
style={{
  transform: this.state.anim.getTranslateTransform()
}}
```
