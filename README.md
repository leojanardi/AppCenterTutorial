# AppCenterTutorial

Instalar a cli do AppCenter como dependência global
npm i -g appcenter-cli

Logar na conta do appcenter
appcenter login

Criar app (React Native)
appcenter apps create -d MeuApp -o Android -p React-Native

Setar app como app em utilização
appcenter apps set-current <ownerName>/<appName>

Criar deployment
appcenter codepush deployment add Production

Verificar os deployments cadastrados
appcenter codepush deployment list

Verificar os deployments cadastrados com suas respectivas chaves
appcenter codepush deployment list -k

Instalar o modulo react-native-code-push
yarn --no-bin-links
yarn add react-native-code-push

The --no-bin-links argument will prevent npm from creating symlinks for any binaries the package might contain.

Atualizar o arquivo android/app/build.gradle, inserindo a linha abaixo, abaixo do apply do react.gradle
apply from: "../../node_modules/react-native-code-push/android/codepush.gradle"

Atualizar o arquivo android/app/src/main/java/com/APPNAME/MainApplication.java incluindo o método abaixo dentro da instância mReactNativeHost
@Override
protected String getJSBundleFile() {
    return CodePush.getJSBundleFile();
}

Atualizar o arquivo android/app/src/main/res/values/strings.xml e incluir as tags abaixo
<string name="appCenterCrashes_whenToSendCrashes" moduleConfig="true" translatable="false">DO_NOT_ASK_JAVASCRIPT</string>
<string name="appCenterAnalytics_whenToEnableAnalytics" moduleConfig="true" translatable="false">ALWAYS_SEND</string>
<string moduleConfig="true" name="CodePushDeploymentKey">CHAVE DO DEPLOY</string>

Na tela principal do app, de preferência a tela de login, dentro do evento componentDidMount() inserir o código abaixo e personalizar de acordo com a necessidade
CodePush.sync({
      installMode: CodePush.InstallMode.ON_NEXT_RESUME,
});

Gerar release no codepush
appcenter codepush release-react -t "*" 

