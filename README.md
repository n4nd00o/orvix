<div align="center">

# Orvix

**Sistema de gestão (ERP) para lojas: PDV, estoque, financeiro, relatórios e loja online num lugar só.**

Em uso numa loja real e vendido como assinatura (várias empresas no mesmo sistema).
*Este repositório é uma vitrine: o código é privado. Os prints usam uma loja de demonstração com dados fictícios.*

![Next.js](https://img.shields.io/badge/Next.js-15-000000?logo=nextdotjs)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-5-2D3748?logo=prisma)
![Playwright](https://img.shields.io/badge/testes-Playwright-2EAD33?logo=playwright&logoColor=white)

**[Ver o site](https://erp-outlet.onrender.com)**

</div>

![Site do Orvix](17-site-topo.png)

## O problema

Lojas pequenas controlam vendas no caderno, estoque na planilha e contas no aplicativo do banco. Nada conversa: o estoque não bate, o lucro do mês é um chute e o fechamento do caixa toma tempo.

## A solução

Um sistema web em que **cada venda baixa o estoque e entra no financeiro sozinha**, com telas pensadas para quem não tem costume com computador: poucos botões, nomes do dia a dia e o que importa logo na primeira tela.

| Início: números do dia, o que está acabando e atalhos | Venda no PDV |
|---|---|
| ![Início](01-inicio.png) | ![PDV](02-pdv.png) |

| Produtos com preço de/por | Lucro e DRE do mês |
|---|---|
| ![Produtos](03-produtos.png) | ![Relatórios](07-relatorios.png) |

| Divulgar no WhatsApp, Instagram e Facebook | Modo escuro |
|---|---|
| ![Divulgar](21-divulgar.png) | ![Modo escuro](12-inicio-escuro.png) |

## Com a cara de cada loja

O dono escolhe as **cores do sistema** (8 temas) e coloca o **nome e a logo da loja** no canto da tela e na guia do navegador. Vale para toda a equipe.

| Aparência: cores, nome e logo | Tema azul |
|---|---|
| ![Aparência](23-aparencia.png) | ![Tema azul](24-tema-azul.png) |

| Tema roxo no PDV | Tema laranja em Produtos |
|---|---|
| ![Tema roxo](25-tema-roxo-pdv.png) | ![Tema laranja](26-tema-laranja-produtos.png) |

<p align="center"><img src="15-celular-pdv.png" width="260" alt="PDV no celular"><br><em>Funciona no celular</em></p>

## Funcionalidades

- **Vendas:** PDV com leitor de código de barras, câmera do celular, Pix com QR Code, cartão, dinheiro e fiado; caixa com abertura, sangria e fechamento; modo só leitor em tela cheia
- **Estoque:** vários locais, transferências, inventário com contagem simultânea, lista de compras por fornecedor, entrada pela nota fiscal (XML da NF-e)
- **Por ramo de negócio:** grade de tamanho e cor, validade e lote, número de série/IMEI, venda por peso
- **Financeiro:** contas a pagar e a receber, cartões a receber por maquininha, DRE
- **Vendas online:** loja com o mesmo estoque, pedido pelo WhatsApp, frete; Mercado Livre e Mercado Pago
- **Divulgação:** tela própria para escolher os produtos e mandar no WhatsApp ou gerar o post do Instagram e do Facebook
- **Aparência por empresa:** 8 temas de cor, nome e logo da loja no menu e na guia do navegador
- **Equipe:** perfis Dono, Administrador, Gerente, Caixa, Estoquista e Consulta

## Decisões técnicas

- **Várias empresas no mesmo banco** com filtro automático por empresa em toda consulta (a consulta falha se a empresa não for identificada); Row Level Security ligado em todas as tabelas para fechar o acesso direto pela API do banco
- **Transações atômicas** em estoque e financeiro (venda, entrada de nota, inventário), testadas com vendas simultâneas
- **Temas sem trocar as telas:** as cores do Tailwind vêm de variáveis CSS e cada empresa troca só as variáveis; a logo é reduzida no navegador e conferida pelo conteúdo do arquivo no servidor (só PNG, JPG ou WebP)
- **Segurança:** verificação em duas etapas, CSRF, limite de tentativas atômico (também contra tentativas em paralelo), limite de tamanho dos pedidos, fila para a checagem de senha sob carga, cabeçalhos de segurança e CSP com nonce
- **Testes de ataque e de carga** em ambiente local: força bruta, XSS, corpo gigante, enxurrada de logins e muitos acessos ao mesmo tempo
- **LGPD:** exportar e excluir os dados pessoais de um cliente, canal do titular, coleta mínima, senhas com bcrypt, backup diário
- **Usabilidade (Heurísticas de Nielsen):** menu de 7 botões com nomes do dia a dia, telas de cada área com os números no topo e botões grandes, telas agrupadas em abas, resposta imediata ao clique e barra de progresso
- **Testes de ponta a ponta** com Playwright (62 testes): venda no PDV, navegação, segurança, LGPD e aparência

## Stack

Next.js (App Router) · React · TypeScript · Tailwind CSS · PostgreSQL · Prisma · Playwright · Docker · Render · Supabase · GitHub Actions

## Autor

**Luiz Fernando Santana**, estudante de Engenharia de Software.
[LinkedIn](https://www.linkedin.com/in/luiz-fernando-santana-trindade/) · [GitHub](https://github.com/n4nd00o)

Desenvolvido com apoio de ferramentas de IA; todo o código é revisado, testado e versionado pelo autor.
