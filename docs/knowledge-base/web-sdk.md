# Como usar o Web SDK de autenticação por telefone

O `nvoip-web-sdk` entrega um popup pronto para fluxos de telefone + código.

Importante: o SDK roda no browser, mas as credenciais da Nvoip devem ficar no backend.

## Instalação

```bash
npm install nvoip-web-sdk@1.0.0
```

## Fluxo seguro

1. O usuário clica em "Validar telefone".
2. O widget chama um endpoint do seu backend.
3. O backend chama a API Nvoip para enviar OTP.
4. O usuário digita o código recebido.
5. O widget chama outro endpoint do backend.
6. O backend valida o código na Nvoip.

## Exemplo frontend

```html
<link rel="stylesheet" href="/node_modules/nvoip-web-sdk/dist/nvoip-auth-widget.css" />
<script src="/node_modules/nvoip-web-sdk/dist/nvoip-auth-widget.js"></script>

<button id="nvoip-auth-trigger">Validar telefone</button>

<script>
  NvoipAuthWidget.mount(document.getElementById("nvoip-auth-trigger"), {
    startVerification: ({ phone }) =>
      fetch("/api/nvoip/auth/start", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ phone })
      }).then((response) => response.json()),
    confirmVerification: ({ sessionId, code, phone }) =>
      fetch("/api/nvoip/auth/confirm", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ sessionId, code, phone })
      }).then((response) => response.json()),
    onSuccess: ({ phone }) => {
      console.log("Telefone validado", phone);
    }
  });
</script>
```

## Demonstração local

Clone https://github.com/Nvoip/nvoip-web-sdk e abra `examples/mock-demo.html`.

O mock usa o código `123456` e não chama a API real.

## Disponibilidade da versão v3

A publicação desta versão no registry ainda depende da regularização das credenciais de publicação. Enquanto ela não estiver disponível, use o código revisado do repositório ou aguarde a publicação; uma versão antiga do pacote não oferece o caminho v3/OAuth descrito aqui.
