# 💬 Atendimento automático no WhatsApp

Modelo de atendente virtual para pequenos negócios de Fortaleza: responde preços, endereço e horário,
anota pedidos de agendamento e chama uma pessoa quando precisa.

🔗 **Simulador ao vivo:** https://talles-eduardo-27.github.io/atendimento-whatsapp/

> Feito com IA (Claude) e revisado por mim. Os negócios, endereços e valores são fictícios.

## O que tem aqui

| Parte | Para que serve |
|---|---|
| `index.html` | Simulador para mostrar a ideia a um cliente: escolha o tipo de negócio (salão, clínica, academia, pet shop, restaurante) e converse como se fosse o cliente. Ao lado aparece o que chega para o dono. Roda no navegador, sem internet e sem custo. |
| `n8n/atendente-whatsapp.json` | Fluxo para importar no **n8n** e colocar para funcionar de verdade, com a API oficial do WhatsApp e um modelo de IA. |

## O problema

Pequenos negócios perdem clientes porque demoram a responder no WhatsApp, principalmente fora do horário.
O cliente quer saber preço, endereço e se tem horário, e desiste quando ninguém responde.

## Como o fluxo do n8n funciona

```
WhatsApp (API oficial da Meta)
   → Gatilho WhatsApp
   → Organizar mensagem (ignora avisos de entregue/lido, pega telefone, nome e texto)
   → É texto?
        sim → Atendente IA (modelo da OpenAI + memória das últimas 10 trocas por telefone)
              → Responder no WhatsApp
        não → Avisar que, por enquanto, só lê texto
```

As regras do atendente ficam no próprio nó **Atendente IA**: só falar do negócio, não inventar preços nem horários,
pedir um dado por vez para agendar e **nunca confirmar um horário sozinho** (a equipe confirma).

O arquivo foi conferido contra as definições dos nós do n8n 2.48 (tipos, versões e parâmetros).

## Como usar com um cliente

1. No n8n, importe `n8n/atendente-whatsapp.json` (menu **Import from File**).
2. Crie as credenciais **WhatsApp Business Cloud** (app na Meta com o número do negócio) e **OpenAI**.
3. Nos dois nós de envio, troque `COLOQUE_O_PHONE_NUMBER_ID` pelo ID do número.
4. No nó **Atendente IA**, troque as informações do salão de exemplo pelas do cliente.
5. Teste com o seu próprio número antes de ativar.

Custos a conferir antes de fechar com o cliente: a hospedagem do n8n, o uso do modelo de IA e a tabela atual de
cobrança da Meta para mensagens do WhatsApp.

## Tecnologias

n8n · API oficial do WhatsApp (Cloud API) · OpenAI · HTML, CSS e JavaScript puro no simulador

## Próximos passos

- Registrar cada pedido numa planilha do Google e avisar o dono por mensagem.
- Mandar lembrete um dia antes do horário marcado.
- Entender áudio (transcrição) além de texto.

---

Projeto de portfólio de [Talles Eduardo](https://github.com/Talles-Eduardo-27). Sites de exemplo usados no simulador:
[salão](https://talles-eduardo-27.github.io/landing-salao/) ·
[clínica](https://talles-eduardo-27.github.io/landing-clinica/) ·
[academia](https://talles-eduardo-27.github.io/landing-academia/) ·
[pet shop](https://talles-eduardo-27.github.io/landing-petshop/) ·
[restaurante](https://talles-eduardo-27.github.io/landing-restaurante/)
