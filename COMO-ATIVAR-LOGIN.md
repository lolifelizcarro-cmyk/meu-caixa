# Como ativar a conta com nome e senha no Meu Caixa

O Meu Caixa salva seus dados no navegador. Para abrir os mesmos dados em qualquer aparelho com nome de usuário e senha, crie um projeto gratuito no Firebase (plano Spark, sem cartão).

1. Abra https://console.firebase.google.com e clique em **Adicionar projeto**. Dê o nome `meu-caixa` e desative o Google Analytics.
2. Em **Criação > Authentication**, clique em **Vamos começar**, escolha **E-mail/senha**, ative a primeira opção (E-mail/senha) e salve. Não precisa ativar o link por e-mail.
3. Em **Criação > Firestore Database**, clique em **Criar banco de dados**, escolha o modo de produção e a região `southamerica-east1`.
4. Na aba **Regras** do Firestore, cole o texto abaixo e clique em **Publicar**:

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

5. Na engrenagem **Configurações do projeto > Geral > Seus apps**, clique no ícone **</>** (Web), registre o app e copie o objeto `firebaseConfig`.
6. Cole esse objeto no arquivo `firebase-config.js` deste repositório, no formato do exemplo, e salve (commit).

Depois de 1 a 2 minutos, o site mostra a tela de login. Cada pessoa só lê e grava os próprios dados, por causa das regras do passo 4.

## Importante

- O nome de usuário vira internamente um e-mail do tipo `nome@meucaixa.app`, que não existe de verdade. Por isso **não há como recuperar a senha**. Anote-a em um lugar seguro.
- Ao clicar em **Sair**, a cópia dos dados neste navegador é apagada. Os dados continuam na sua conta.
- O botão "Usar sem conta" mantém o uso só neste navegador, sem sincronizar.
