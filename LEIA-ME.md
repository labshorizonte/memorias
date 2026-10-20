# Memória 100 - Pacote para a Play Store

Conteúdo da pasta:
- `www/` - o jogo (index.html), manifest, service worker (offline) e ícones
- `assets/` - ícone e splash em alta resolução (para gerar os ícones do Android)
- `loja/` - ícone 512, imagem de destaque, política de privacidade e textos da ficha
- `capacitor.config.json` e `package.json` - configuração para gerar o app Android

ID do app (package name): `br.com.animeplayvideo.memoria100`
Esse ID não pode mais ser trocado depois de publicado.

---

## Caminho A - Com computador (Capacitor + Android Studio)

Requisitos: Node.js (versão LTS) e Android Studio instalados.

1. Abra o terminal dentro desta pasta e instale:
   ```
   npm install @capacitor/core @capacitor/cli @capacitor/android
   npm install -D @capacitor/assets
   ```
2. Crie o projeto Android e gere os ícones:
   ```
   npx cap add android
   npx capacitor-assets generate --android
   npx cap sync android
   ```
3. Abra no Android Studio:
   ```
   npx cap open android
   ```
4. Teste: conecte o celular com depuração USB (ou use o emulador) e clique em Run.
5. Gere o arquivo de publicação (AAB):
   Build > Generate Signed App Bundle / APK > Android App Bundle.
   - Crie uma nova chave (keystore) e **guarde o arquivo e as senhas em local seguro**. Sem ela você não consegue atualizar o app depois.
   - Escolha o modo `release`.
6. O arquivo `.aab` gerado é o que você envia ao Play Console.

Antes de gerar o AAB, abra `android/app/build.gradle` e confira `versionCode` (começa em 1; aumente a cada atualização) e `versionName`.

## Caminho B - Sem computador (PWABuilder)

1. Hospede a pasta `www/` em um endereço HTTPS (por exemplo, um subdomínio do seu domínio, como memoria.animeplayvideo.com.br).
2. Acesse pwabuilder.com, cole o endereço e gere o pacote Android (AAB).
3. Guarde a chave de assinatura que ele fornecer.

(Confirme os passos atuais no próprio site, pois a ferramenta pode mudar.)

---

## Publicação no Google Play Console

1. Crie a conta de desenvolvedor (taxa única de US$ 25) e conclua a verificação de identidade.
2. Crie o app: nome, idioma (Português do Brasil), tipo "Jogo", gratuito.
3. Preencha a ficha usando `loja/textos-da-loja.md` e envie as imagens da pasta `loja/`.
4. Publique a política de privacidade (`loja/politica-de-privacidade.html`) em um link público e informe o link. Lembre de colocar seu e-mail de contato no arquivo antes.
5. Responda o questionário de classificação indicativa e a seção Segurança dos dados.
6. Envie o `.aab` em um teste interno/fechado primeiro.
7. Contas pessoais novas costumam precisar de um teste fechado com testadores por um período mínimo (a regra era 12 testadores por 14 dias; confirme o valor atual no Play Console).
8. Depois de cumprir os requisitos, solicite o acesso à produção e envie para análise.

## Lista de conferência final
- [ ] E-mail de contato colocado na política de privacidade
- [ ] Política publicada em link público
- [ ] Pelo menos 2 capturas de tela reais do jogo
- [ ] Keystore e senhas guardadas em backup
- [ ] `.aab` assinado e testado em um aparelho real
