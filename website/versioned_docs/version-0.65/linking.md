---
id: linking
title: Linking
---

import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem'; import constants from '@site/core/TabsConstants';

 <div className="banner-native-code-required"> 
 <h3> Projetos com código nativo somente </h3> 
 <p> 
 A seção a seguir só se aplica a projetos com código nativo exposto. Se você estiver usando o fluxo de trabalho gerenciado <code> expo-cli </code>, consulte o guia sobre <a href="http://docs.expo.io/versions/latest/workflow/linking/"> Vinculando </a> na documentação da Expo para obter a alternativa apropriada.
 </p> 
 </div> 

O `Linking` oferece uma interface geral para interagir com links de aplicativos de entrada e saída.

Cada Link (URL) tem um Esquema de URL, alguns sites são prefixados com `https: //` ou `http: //` e o `http` é o Esquema de URL. Vamos chamá-lo de esquema para abreviar.

Além de `https`, você provavelmente também está familiarizado com o esquema `mailto`. Quando você abre um link com o esquema mailto, seu sistema operacional abrirá um aplicativo de e-mail instalado. Da mesma forma, existem esquemas para fazer chamadas telefônicas e enviar SMS. Leia mais sobre os esquemas de [URL embutido] (#built -in-url-schemes) abaixo.

Like using the mailto scheme, it's possible to link to other applications by using custom url schemes. For example, when you get a **Magic Link** email from Slack, the **Launch Slack** button is an anchor tag with an href that looks something like: `slack://secret/magic-login/other-secret`. Like with Slack, you can tell the operating system that you want to handle a custom scheme. When the Slack app opens, it receives the URL that was used to open it. This is often referred to as deep linking. Read more about how to [get the deep link](#get-the-deep-link) into your app.

O esquema de URL personalizado não é a única maneira de abrir seu aplicativo no celular. Você não quer usar um esquema de URL personalizado nos links do e-mail porque os links seriam quebrados na área de trabalho. Em vez disso, você deseja usar links `https` regulares, como `https://www.myapp.io/records/1234546 `. e no celular você deseja que esse link abra seu aplicativo. O Android chama de**Deep Links** (Links universais - iOS).

### Built-in URL Schemes

Conforme mencionado na introdução, existem alguns esquemas de URL para a funcionalidade principal que existem em todas as plataformas. A seguir, uma lista não exaustiva, mas abrange os esquemas mais usados.

| Scheme           | Descrição                                | iOS | Android |
| ---------------- | ------------------------------------------ | --- | ------- |
| `mailto`         | Abra o aplicativo de e-mail, por exemplo: mailto: support@expo.io | ✅  | ✅      |
| `tel`            | Aplicativo para telefone aberto, por exemplo: tel: +123456789         | ✅  | ✅      |
| `sms`            | Abra o aplicativo SMS, por exemplo: sms: +123456789           | ✅  | ✅      |
| `https` / `http` | Abra o aplicativo de navegador da web, por exemplo: https://expo.io  | ✅  | ✅      |

### Ativando links profundos

Se você quiser ativar links diretos em seu aplicativo, leia o guia abaixo:

<Tabs groupId="syntax" defaultValue={constants.defaultPlatform} values={constants.platforms}>
<TabItem value="android">

> Para obter instruções sobre como adicionar suporte para links diretos no Android, consulte [Habilitando links diretos para conteúdo do aplicativo - Adicionar filtros de intenção para seus links diretos] (http://developer.android.com/training/app-indexing/deep-linking.html#adding-filters).

Se você deseja receber o intent em uma instância existente de MainActivity, você pode definir o `launchMode` de MainActivity como `SingleTask` em `AndroidManifest.xml`. Consulte a documentação [`<activity>`] (http://developer.android.com/guide/topics/manifest/activity-element.html) para obter mais informações.

```xml
<activity
  android:name=".MainActivity"
  android:launchMode="singleTask">
```

</TabItem>
<TabItem value="ios">

> **NOTA: ** No iOS, você precisará adicionar a pasta `LinkingIOS` em seus caminhos de pesquisa de cabeçalho, conforme descrito na etapa 3 [aqui] (linking-libraries-ios #step -3). Se você também quiser ouvir os links de aplicativos recebidos durante a execução do aplicativo, você precisará adicionar as seguintes linhas ao seu `*AppDelegate.m`:

```objectivec
// iOS 9.x or newer
#import <React/RCTLinkingManager.h>

- (BOOL)application:(UIApplication *)application
   openURL:(NSURL *)url
   options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
{
  return [RCTLinkingManager application:application openURL:url options:options];
}
```

Se você estiver segmentando o iOS 8.x ou mais antigo, poderá usar o seguinte código:

```objectivec
// iOS 8.x or older
#import <React/RCTLinkingManager.h>

- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
  return [RCTLinkingManager application:application openURL:url
                      sourceApplication:sourceApplication annotation:annotation];
}
```

Se seu aplicativo estiver usando [Links universais] (https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/AppSearch/UniversalLinks.html), você precisará adicionar o seguinte código também:

```objectivec
- (BOOL)application:(UIApplication *)application continueUserActivity:(nonnull NSUserActivity *)userActivity
 restorationHandler:(nonnull void (^)(NSArray<id<UIUserActivityRestoring>> * _Nullable))restorationHandler
{
 return [RCTLinkingManager application:application
                  continueUserActivity:userActivity
                    restorationHandler:restorationHandler];
}
```

</TabItem>
</Tabs>

### Como lidar com links profundos

Existem duas maneiras de lidar com URLs que abrem seu aplicativo.

#### 1. Se o aplicativo já estiver aberto, o aplicativo estará em primeiro plano e um evento “url” de vinculação será acionado

Você pode lidar com esses eventos com `linking.addEventListener ('url', callback) `- ele chama `callback ({url,})` com o URL vinculado

#### 2. Se o aplicativo ainda não estiver aberto, ele será aberto e o URL será passado como o URL inicial

Você pode lidar com esses eventos com `linking.getInitialUrl () `- ele retorna uma Promise que resolve para o URL, se houver um.

---

## Exemplo

### Links abertos e links diretos (links universais)

```SnackPlayer name=Linking%20Function%20Component%20Example&supportedPlatforms=ios,android
import React, { useCallback } from "react";
import { Alert, Button, Linking, StyleSheet, View } from "react-native";

const supportedURL = "https://google.com";

const unsupportedURL = "slack://open?team=123456";

const openURLButton = ({url, crianças}) => {
 const handlePress = useCallback (async () => {
 //Verificando se o link é compatível com links com esquema de URL personalizado.
 const suportado = await linking.canOpenURL (url);

    if (suportado) {
 //Abrindo o link com algum aplicativo, se o esquema de URL for “http”, o link da web deve ser aberto
 //por algum navegador no celular
 aguarde o linking.openURL (url);
 } else {
 Alert.alert (`Não sei como abrir este URL: $ {url} `);
 }
  }, [url]);

  return <Button title={children} onPress={handlePress} />;
};

const App = () => {
  return (
    <View style={styles.container}>
      <OpenURLButton url={supportedURL}>Open Supported URL</OpenURLButton>
      <OpenURLButton url={unsupportedURL}>Open Unsupported URL</OpenURLButton>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
});

export default App;
```

### Open Custom Settings

```SnackPlayer name=Linking%20Function%20Component%20Example&supportedPlatforms=ios,android
import React, { useCallback } from "react";
import { Button, Linking, StyleSheet, View } from "react-native";

const OpenSettingsButton = ({ children }) => {
  const handlePress = useCallback(async () => {
    // Open the custom settings if the app has one
    await Linking.openSettings();
  }, []);

  return <Button title={children} onPress={handlePress} />;
};

const App = () => {
  return (
    <View style={styles.container}>
      <OpenSettingsButton>Open Settings</OpenSettingsButton>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
});

export default App;
```

### Obtenha o Deep Link

```SnackPlayer name=Linking%20Function%20Component%20Example&supportedPlatforms=ios,android
import React, { useState, useEffect } from "react";
import { Linking, StyleSheet, Text, View } from "react-native";

const useMount = func => useEffect(() => func(), []);

const useInitialURL = () => {
  const [url, setUrl] = useState(null);
  const [processing, setProcessing] = useState(true);

  useMount(() => {
    const getUrlAsync = async () => {
      // Get the deep link used to open the app
      const initialUrl = await Linking.getInitialURL();

      // The setTimeout is just for testing purpose
      setTimeout(() => {
        setUrl(initialUrl);
        setProcessing(false);
      }, 1000);
    };

    getUrlAsync();
  });

  return { url, processing };
};

const App = () => {
  const { url: initialUrl, processing } = useInitialURL();

  return (
    <View style={styles.container}>
      <Text>
        {processing
          ? `Processing the initial url from a deep link`
          : `The deep link is: ${initialUrl || "None"}`}
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
});

export default App;
```

### Send Intents (Android)

```SnackPlayer name=Linking%20Function%20Component%20Example&supportedPlatforms=android
import React, { useCallback } from "react";
import { Alert, Button, Linking, StyleSheet, View } from "react-native";

const SendIntentButton = ({ action, extras, children }) => {
  const handlePress = useCallback(async () => {
    try {
      await Linking.sendIntent(action, extras);
    } catch (e) {
      Alert.alert(e.message);
    }
  }, [action, extras]);

  return <Button title={children} onPress={handlePress} />;
};

const App = () => {
  return (
    <View style={styles.container}>
      <SendIntentButton action="android.intent.action.POWER_USAGE_SUMMARY">
        Power Usage Summary
      </SendIntentButton>
      <SendIntentButton
        action="android.settings.APP_NOTIFICATION_SETTINGS"
        extras={[
          { "android.provider.extra.APP_PACKAGE": "com.facebook.katana" },
        ]}
      >
        App Notification Settings
      </SendIntentButton>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: "center", alignItems: "center" },
});

export default App;
```

# Referência

## Métodos

### `addEventListener()`

```jsx
addEventListener(type, handler);
```

Adicione um manipulador a Linking changes ouvindo o tipo de evento `url` e fornecendo o manipulador.

---

### `canOpenURL()`

```jsx
canOpenURL(url);
```

Determine se um aplicativo instalado pode ou não lidar com um determinado URL.

O método retorna um objeto `Promise`. Quando é determinado se o URL fornecido pode ou não ser tratado, a promessa é resolvida e o primeiro parâmetro é se ele pode ou não ser aberto.

O `Promise` será rejeitado no Android se for impossível verificar se o URL pode ser aberto, e no iOS se você não adicionou o esquema específico na chave `LSApplicationQueriesSchemes` dentro de `Info.plist` (veja abaixo).

**Parâmetros: **

| Nome                                                     | Tipo   | Descrição      |
| -------------------------------------------------------- | ------ | ---------------- |
| url <div className="label basic required">Required</div> | string | The URL to open. |

> Para URLs da web, o protocolo (`"http: //"`, `"https: //"`) deve ser definido de acordo!

> Esse método tem limitações no iOS 9+. De [a documentação oficial da Apple] (https://developer.apple.com/documentation/uikit/uiapplication/1622952-canopenurl):
>> - Se o aplicativo estiver vinculado a uma versão anterior do iOS, mas estiver sendo executado no iOS 9.0 ou posterior, você poderá chamar esse método até 50 vezes. Depois de atingir esse limite, as chamadas subsequentes sempre retornam falsas. Se o usuário reinstalar ou atualizar o aplicativo, o iOS redefine o limite.
>> A partir do iOS 9, seu aplicativo também precisa fornecer a chave `LSApplicationQueriesSchemes` dentro de `Info.plist` ou `CanOpenUrl () `sempre retornará `false`.

---

### `getInitialURL()`

```jsx
getInitialURL();
```

Se o lançamento do aplicativo foi acionado por um link do aplicativo, ele fornecerá o URL do link, caso contrário, fornecerá `null`.

> Para oferecer suporte a links diretos no Android, consulte http://developer.android.com/training/app-indexing/deep-linking.html#handling-intents

> GetInitialUrl pode retornar `null` enquanto a depuração está ativada. Desative o depurador para garantir que ele seja aprovado.

---

### `openSettings()`

```jsx
openSettings();
```

Abra o aplicativo Configurações e exiba as configurações personalizadas do aplicativo, se houver.

---

### `openURL()`

```jsx
openURL(url);
```

Tente abrir o `url` fornecido com qualquer um dos aplicativos instalados.

Você pode usar outros URLs, como um local (por exemplo, “geo:37.484847, -122.148386" no Android ou" http://maps.apple.com/?ll=37.484847,-122.148386 "no iOS), um contato ou qualquer outro URL que possa ser aberto com os aplicativos instalados.

O método retorna um objeto `Promise`. Se o usuário confirmar a caixa de diálogo aberta ou o URL abrir automaticamente, a promessa será resolvida. Se o usuário cancelar a caixa de diálogo aberta ou não houver aplicativos registrados para o url, a promessa será rejeitada.

**Parâmetros: **

| Nome                                                     | Tipo   | Descrição      |
| -------------------------------------------------------- | ------ | ---------------- |
| url <div className="label basic required">Required</div> | string | O URL a ser aberto. |

> Esse método falhará se o sistema não souber como abrir o URL especificado. Se você estiver passando um URL não http (s), é melhor verificar `canOpenURL () `primeiro.

> Para URLs da web, o protocolo (`"http: //"`, `"https: //"`) deve ser definido de acordo!

> Este método pode se comportar de maneira diferente em um simulador, por exemplo, links `"tel: "`não podem ser manipulados no simulador iOS, pois não há acesso ao aplicativo discador.

---

### `removeEventListener()`

```jsx
removeEventListener(type, handler);
```

> **Descontinuado.** Use o método `remove () `na assinatura de evento retornada por [`addEventListener ()`] (#addeventlistener).

---

### `sendIntent()` <div class="label android">Android</div>

```jsx
sendIntent(action, extras);
```

Inicie uma intenção do Android com extras.

**Parâmetros: **

| Nome                                                        | Tipo                                                     |
| ----------------------------------------------------------- | -------------------------------------------------------- |
| action <div className="label basic required">Required</div> | string                                                   |
| extras                                                      | array of `{key: string, value: string, number, boolean}` |
