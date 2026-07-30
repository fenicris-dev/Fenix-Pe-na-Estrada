# Regra de segurança multiuser — Firestore (Pé na Estrada)

## A ideia

Cada usuário só enxerga e só mexe nos próprios dados. Ninguém — nem por engano, nem tentando — consegue ler ou escrever no espaço de outro usuário. Isso é garantido no servidor do Firebase, então nem depende do código do app estar certo: mesmo que alguém tente burlar pelo navegador, a regra barra.

**Login escolhido:** Email e senha (Firebase Authentication).

## Estrutura de dados recomendada

Tudo dentro de uma coleção `users`, organizado pelo `uid` (o ID único que o Firebase gera pra cada conta logada):

```
users/{uid}/corridas/{corridaId}
users/{uid}/abastecimentos/{abastecimentoId}
users/{uid}/veiculos/{placa}
users/{uid}/config/geral        ← doc único com enderecoCasa, destinosFavoritos, veiculoAtivo, configBusca
```

Ou seja: nada de coleção "solta" com todo mundo misturado — cada usuário tem sua própria "gaveta" (`users/{uid}/...`), com todas as subcoleções (corridas, abastecimentos, veículos, config) dentro dela.

## A regra

No Firebase Console → seu projeto (`fenix-pe-na-estrada`) → **Firestore Database** → aba **Regras**, apague o que tiver lá e cole:

```
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {

    // Cada usuário só acessa o que está dentro da própria pasta users/{uid}/...
    // O {document=**} cobre TODAS as subcoleções (corridas, abastecimentos, veiculos, config)
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }

    // Qualquer coisa fora de users/{uid}/ fica bloqueada por padrão
  }
}
```

Clique em **Publicar**.

### O que essa regra garante
- `request.auth != null` → só deixa passar quem está logado (ninguém anônimo, ninguém sem conta).
- `request.auth.uid == userId` → e mesmo logado, só deixa mexer na própria pasta (`users/SEU_UID/...`), nunca na de outro parceiro.
- Tudo que não está dentro de `users/{uid}/` fica **bloqueado por padrão** — o Firestore nega por padrão o que a regra não libera explicitamente.

## O que falta habilitar no Console (antes da regra funcionar)

1. **Firestore Database** → criar o banco (se ainda não criado) → modo produção (não "modo de teste", que libera tudo por 30 dias e depois trava geral).
2. **Authentication** → aba **Sign-in method** → habilitar **Email/senha**.
3. Colar a regra acima e publicar.

## O que ainda não está pronto (próximos passos, quando for integrar no código)

Essa regra já deixa o banco seguro, mas o app (`Pé na Estrada`) ainda salva tudo em `localStorage`, não no Firestore. Quando for a hora de integrar:

- Vai precisar de uma tela de login (email/senha) antes de liberar o app.
- Cada leitura/escrita que hoje é `localStorage.getItem/setItem` vira uma chamada ao Firestore (`getDoc`, `setDoc`, etc.), sempre usando `users/{uid}/...` como caminho.
- Dá pra manter o `localStorage` como cache local (abre rápido, funciona offline) e sincronizar com o Firestore em segundo plano — o Firestore SDK já faz isso sozinho se você usar `enableIndexedDbPersistence`.

Não precisa se preocupar com essa parte agora — a regra já está pronta e segura pra quando você (ou eu) formos fazer essa integração.
