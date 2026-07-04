# IrrigaBerry — App de Irrigação

App web (PWA) do sistema de irrigação/fertirrigação para morango semi-hidropônico.

**Código único, configuração por cliente.** Esta mesma página serve todos os
clientes. O que muda por cliente é só a config lida em runtime (broker MQTT,
usuário/senha, nome), injetada na primeira abertura por um **link único** gerado
no provisionamento do kit:

```
https://irrigaberry.github.io/?broker=HOST.ts.net&port=443&user=webapp&pass=SENHA&cliente=Nome
```

O app lê esses parâmetros, salva no `localStorage` do aparelho e **apaga a query
da URL** (a senha não fica na barra/histórico). Reaberturas seguintes conectam
sozinhas com o que ficou salvo.

Cada cliente tem seu próprio Raspberry Pi (broker Mosquitto isolado, exposto via
Tailscale Funnel com TLS). O isolamento vem do hostname do broker + credencial —
os `device_id` são padronizados e iguais em todos os kits.

## Deploy

GitHub Pages serve direto da branch `main` (raiz). `git push` = todos os clientes
recebem a atualização.
