---
id: permissionsandroid
title: PermissionsAndroid
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

 <div className="banner-native-code-required"> 
 <h3> Projeto com código nativo necessário </h3> 
 <p> 
 A seção a seguir só se aplica a projetos com código nativo exposto. Se você estiver usando o fluxo de trabalho gerenciado <code> expo-cli </code>, consulte o guia sobre <a href="https://docs.expo.io/versions/latest/sdk/permissions/"> Permissões </a> na documentação da Expo para obter a alternativa apropriada.
 </p> 
 </div> 

`permissionsAndroid` fornece acesso ao novo modelo de permissões do Android M. As chamadas permissões “normais” são concedidas por padrão quando o aplicativo é instalado, desde que apareçam em `AndroidManifest.xml`. No entanto, permissões “perigosas” exigem um prompt de diálogo. Você deve usar este módulo para essas permissões.

Em dispositivos antes do SDK versão 23, as permissões são concedidas automaticamente se aparecerem no manifesto, então `check` sempre deve resultar em `true` e `request` deve sempre resolver para `permissionsAndroid.results.granted`.

Se um usuário tiver desativado anteriormente uma permissão solicitada por você, o sistema operacional aconselhará seu aplicativo a mostrar uma justificativa para precisar da permissão. O argumento opcional `rationale` mostrará um prompt de diálogo somente se necessário - caso contrário, o prompt de permissão normal aparecerá.

### Exemplo

<Tabs groupId="syntax" defaultValue={constants.defaultSyntax} values={constants.syntax}>
<TabItem value="functional">

```SnackPlayer name=PermissionsAndroid%20Example&supportedPlatforms=android
import React from "react";
import { Button, PermissionsAndroid, SafeAreaView, StatusBar, StyleSheet, Text, View } from "react-native";

const requestCameraPermission = async () => {
  try {
    const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.CAMERA,
      {
        title: "Cool Photo App Camera Permission",
        message:
          "Cool Photo App needs access to your camera " +
          "so you can take awesome pictures.",
        buttonNeutral: "Ask Me Later",
        buttonNegative: "Cancel",
        buttonPositive: "OK"
      }
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
      console.log("You can use the camera");
    } else {
      console.log("Camera permission denied");
    }
  } catch (err) {
    console.warn(err);
  }
};

const App = () => (
  <View style={styles.container}>
    <Text style={styles.item}>Try permissions</Text>
    <Button title="request permissions" onPress={requestCameraPermission} />
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: StatusBar.currentHeight,
    backgroundColor: "#ecf0f1",
    padding: 8
  },
  item: {
    margin: 24,
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  }
});

export default App;
```

</TabItem>
<TabItem value="classical">

```SnackPlayer name=PermissionsAndroid%20Example&supportedPlatforms=android
import React, { Component } from "react";
import { Button, PermissionsAndroid, SafeAreaView, StatusBar, StyleSheet, Text, View } from "react-native";

const requestCameraPermission = async () => {
  try {
    const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.CAMERA,
      {
        title: "Cool Photo App Camera Permission",
        message:
          "Cool Photo App needs access to your camera " +
          "so you can take awesome pictures.",
        buttonNeutral: "Ask Me Later",
        buttonNegative: "Cancel",
        buttonPositive: "OK"
      }
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
      console.log("You can use the camera");
    } else {
      console.log("Camera permission denied");
    }
  } catch (err) {
    console.warn(err);
  }
};

class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.item}>Try permissions</Text>
        <Button title="request permissions" onPress={requestCameraPermission} />
      </View>
    );
  }
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: StatusBar.currentHeight,
    backgroundColor: "#ecf0f1",
    padding: 8
  },
  item: {
    margin: 24,
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  }
});

export default App;
```

</TabItem>
</Tabs>

### Permissões que exigem a solicitação do usuário

Disponível como constantes em `permissionsAndroid.permissions`:

- `READ_CALENDAR`: 'android.permission.READ_CALENDAR'
- `WRITE_CALENDAR`: 'android.permission.WRITE_CALENDAR'
- `CAMERA`: 'android.permission.CAMERA'
- `READ_CONTACTS`: 'android.permission.READ_CONTACTS'
- `WRITE_CONTACTS`: 'android.permission.WRITE_CONTACTS'
- `GET_ACCOUNTS`: 'android.permission.GET_ACCOUNTS'
- `ACCESS_FINE_LOCATION`: 'android.permission.ACCESS_FINE_LOCATION'
- `ACCESS_COARSE_LOCATION`: 'android.permission.ACCESS_COARSE_LOCATION'
- `RECORD_AUDIO`: 'android.permission.RECORD_AUDIO'
- `READ_PHONE_STATE`: 'android.permission.READ_PHONE_STATE'
- `CALL_PHONE`: 'android.permission.CALL_PHONE'
- `READ_CALL_LOG`: 'android.permission.READ_CALL_LOG'
- `WRITE_CALL_LOG`: 'android.permission.WRITE_CALL_LOG'
- `ADD_VOICEMAIL`: 'com.android.voicemail.permission.ADD_VOICEMAIL'
- `USE_SIP`: 'android.permission.USE_SIP'
- `PROCESS_OUTGOING_CALLS`: 'android.permission.PROCESS_OUTGOING_CALLS'
- `BODY_SENSORS`: 'android.permission.BODY_SENSORS'
- `SEND_SMS`: 'android.permission.SEND_SMS'
- `RECEIVE_SMS`: 'android.permission.RECEIVE_SMS'
- `READ_SMS`: 'android.permission.READ_SMS'
- `RECEIVE_WAP_PUSH`: 'android.permission.RECEIVE_WAP_PUSH'
- `RECEIVE_MMS`: 'android.permission.RECEIVE_MMS'
- `READ_EXTERNAL_STORAGE`: 'android.permission.READ_EXTERNAL_STORAGE'
- `WRITE_EXTERNAL_STORAGE`: 'android.permission.WRITE_EXTERNAL_STORAGE'

### Strings de resultado para solicitar permissões

Disponível como constantes em `permissionsAndroid.results`:

- `GRANTED`: 'granted'
- `DENIED`: 'denied'
- `NEVER_ASK_AGAIN`: 'never_ask_again'

---

# Referência

## Métodos

### `constructor()`

```jsx
constructor();
```

---

### `check()`

```jsx
check(permission);
```

Retorna uma promessa resolvendo para um valor booleano se as permissões especificadas foram concedidas.

**Parâmetros: **

| Nome       | Tipo   | Obrigatório | Descrição                  |
| ---------- | ------ | -------- | ---------------------------- |
| permission | string | sim      | A permissão para verificar. |

---

### `request()`

```jsx
request(permission, [rationale]);
```

Solicita que o usuário ative uma permissão e retorna uma promessa resolvendo para um valor de string (consulte as cadeias de resultados acima) indicando se o usuário permitiu ou negou a solicitação ou não deseja ser solicitado novamente.

Se `rationale` for fornecido, esta função verifica com o SO se é necessário mostrar uma caixa de diálogo explicando por que a permissão é necessária (https://developer.android.com/training/permissions/requesting.html#explain) e, em seguida, mostra a caixa de diálogo de permissão do sistema.

**Parâmetros: **

| Nome       | Tipo   | Obrigatório | Descrição                |
| ---------- | ------ | -------- | -------------------------- |
| permission | string | sim      | A permissão para solicitar. |
| rationale  | object | Não       | Veja `rationale` abaixo.     |

**Racional: **

| Nome           | Tipo   | Obrigatório | Descrição                      |
| -------------- | ------ | -------- | -------------------------------- |
| title          | string | Yes      | O título da caixa de diálogo.         |
| message        | string | Yes      | A mensagem da caixa de diálogo.       |
| buttonPositive | string | Yes      | O texto do botão positivo. |
| buttonNegative | string | No       | O texto do botão negativo. |
| buttonNeutral  | string | No       | O texto do botão neutro.  |

---

### `requestMultiple()`

```jsx
requestMultiple(permissions);
```

Solicita que o usuário habilite várias permissões na mesma caixa de diálogo e retorna um objeto com as permissões como chaves e strings como valores (consulte as cadeias de resultados acima) indicando se o usuário permitiu ou negou a solicitação ou não deseja ser solicitado novamente.

**Parâmetros: **

| Nome        | Tipo  | Obrigatório | Descrição                      |
| ----------- | ----- | -------- | -------------------------------- |
| permissions | array | sim      | Matriz de permissões a serem solicitadas. |
