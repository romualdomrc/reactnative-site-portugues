---
id: animatedvalue
title: Animated.Value
---

Valor padrão para dirigir animações. Um `Animated.Value` pode conduzir várias propriedades de forma sincronizada, mas só pode ser acionado por um mecanismo por vez. Usar um novo mecanismo (por exemplo, iniciar uma nova animação ou chamar `setValue`) interromperá os anteriores.

Normalmente inicializado com `new Animated.Value (0); `

---

# Referência

## Métodos

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

### `interpolate()`

```jsx
interpolate(config);
```

Interpola o valor antes de atualizar a propriedade, por exemplo, mapeamento de 0-1 a 0-10.

See `AnimatedInterpolation.js`

**Parâmetros: **

| Nome   | Tipo   | Obrigatório | Descrição |
| ------ | ------ | -------- | ----------- |
| config | object | sim      | Veja abaixo.  |

O objeto `config` é composto pelas seguintes chaves:

- `InputRange`: uma matriz de números
- `OutputRange`: uma matriz de números ou strings
- `easing` (opcional): uma função que retorna um número, dado um número de entrada
- `extrapolate` (opcional): uma string como 'extend', 'identity' ou 'clamp'
- `ExtrapolateLeft` (opcional): uma string como 'extend', 'identity' ou 'clamp'
- `ExtrapolateRight` (opcional): uma string como 'extend', 'identity' ou 'clamp'

---

### `animate()`

```jsx
animate(animation, callback);
```

Normalmente usado apenas internamente, mas pode ser usado por uma classe Animation personalizada.

**Parâmetros: **

| Nome      | Tipo      | Obrigatório | Descrição         |
| --------- | --------- | -------- | ------------------- |
| animation | Animation | Yes      | See `Animation.js`. |
| callback  | function  | sim      | Função de retorno de chamada.  |

---

### `stopTracking()`

```jsx
stopTracking();
```

Normalmente usado apenas internamente.

---

### `track()`

```jsx
track(tracking);
```

Normalmente usado apenas internamente.

**Parâmetros: **

| Nome     | Tipo         | Obrigatório | Descrição           |
| -------- | ------------ | -------- | --------------------- |
| tracking | AnimatedNode | sim      | Consulte `AnimatedNode.js` |
