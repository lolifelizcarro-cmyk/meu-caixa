# Como ativar o login com Google no Meu Caixa

O Meu Caixa salva seus dados no navegador. Para abrir os mesmos dados em qualquer aparelho com a sua conta Google, crie um projeto gratuito no Firebase (plano Spark, sem cartão).

1. Abra https://console.firebase.google.com e clique em **Adicionar projeto**. Dê o nome `meu-caixa` e desative o Google Analytics.
2. Em **Criação > Authentication**, clique em **Vamos começar**, escolha **Google**, ative, selecione seu e-mail de suporte e salve.
3. Em Authentication, abra **Configurações > Domínios autorizados** e adicione `lolifelizcarro-cmyk.github.io`.
4. Em **Criação > Firestore Database**, clique em **Criar banco de dados**, escolha o modo de produção e a região `southamerica-east1`.
5. Na aba **Regras** do Firestore, cole o texto abaixo e clique em **Publicar**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

6. Na engrenagem **Configurações do projeto > Geral > Seus apps**, clique no ícone **</>** (Web), registre o app e copie o objeto `firebaseConfig`.
7. Cole esse objeto no arquivo `firebase-config.js` deste repositório, no formato do exemplo, e salve (commit).

Depois de 1 a 2 minutos, o botão **Entrar com Google** aparece no topo do site. Cada pessoa só lê e grava os próprios dados, por causa das regras do passo 5.
