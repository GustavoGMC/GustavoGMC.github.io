# Roteamento estático com PfSense

Neste laboratório, temos o objetivo de conectar duas redes (amarela e rosa) através de uma conexão direta, neste caso, um cabo.

![](https://substackcdn.com/image/fetch/$s_!vJZ7!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F403906da-e692-473b-86af-af441cdbffd4_2048x1273.png)

Neste ambiente, já temos as 4 subnets configuradas e se comunicando com a internet, os firewalls não se comunicam através da interface “*wan*”.

# **Configuração da interface P2P**

A interface P2P será a responsável por manter a comunicação direta entre as redes amarela e rosa. Vamos configurar ambas as interfaces como IPV4 estático fazendo uso dos seguintes endereços:

![](https://substackcdn.com/image/fetch/$s_!2A8l!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9d737e45-a4a8-4bce-8759-9e38cb093809_404x76.png)

Configuração realizada no device da rede amarela, para a rede rosa, usaremos o endereço com final 2.

![Configuração realizada no device da rede amarela, para a rede rosa, usaremos o endereço com final 2.](https://substackcdn.com/image/fetch/$s_!kiI2!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F72397f24-4664-4f46-b6f1-0d954cb18321_1140x797.png)

Configuração realizada no device da rede amarela, para a rede rosa, usaremos o endereço com final 2.

> **Importante:** Para estas interfaces, serão desabilitadas as opções: “*Block private networks and loopback addresses*” e “*Block bogon networks*”
> 

# **Configuração dos Gateways**

Agora, vamos configurar os Gateways responsáveis pela comunicação entre os firewalls.

![](https://substackcdn.com/image/fetch/$s_!2A8l!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9d737e45-a4a8-4bce-8759-9e38cb093809_404x76.png)

O PfSense permite a configuração de duas maneiras, a primeira, diretamente na configuração da interface, onde é adicionado o IP e a descrição, de forma fácil e objetiva:

![](https://substackcdn.com/image/fetch/$s_!uyfO!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5fcc6bd3-c379-425e-af2e-2102482a23e7_900x371.png)

A segunda forma, mais completa, oferece opções mais avançadas, como IP de monitoramento, peso, status, etc.

Para termos acesso à tela de configuração seguimos:

1. No menu superior: *System→Routing*;
2. Na tela de Gateways clicamos em *Add*.

Na tela de configuração, vamos inserir, basicamente os mesmos dados que na versão simplificada, poŕem, vamos identificar qual interface utilizará o gateway.

Neste laboratório, os demais campos, podemos deixar na configuração padrão.

![Neste laboratório, os demais campos, podemos deixar na configuração padrão.](https://substackcdn.com/image/fetch/$s_!OToG!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3f5765fc-9517-4584-98f3-eadac2a6e795_1138x380.png)

Neste laboratório, os demais campos, podemos deixar na configuração padrão.

# **Rotas estáticas**

Ainda no menu de roteamento do PfSense, devemos selecionar a opção “*Static Routes*” e devemos criar uma nova rota estática, conforme as imagens abaixo:

Configuração de rota estática no FW Amarelo.

![Configuração de rota estática no FW Amarelo.](https://substackcdn.com/image/fetch/$s_!3PCb!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F7462f155-b491-4b99-bff7-289c2f03c935_1138x423.png)

Configuração de rota estática no FW Amarelo.

Configuração de rota estática no FW Rosa.

![Configuração de rota estática no FW Rosa.](https://substackcdn.com/image/fetch/$s_!IX5b!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5e76a9dc-b3ad-460c-9080-0046d08ef759_1138x426.png)

Configuração de rota estática no FW Rosa.

# **Regras de Firewall**

> Esta etapa pode variar de configuração para configuração, interfaces com liberação total não precisam de uma regra específica, verifique seu Firewall e as políticas de segurança a serem seguidas. Não me aprofundarei neste tópico.
> 

Vamos criar regras para comunicação entre as redes, conforme abaixo:

![](https://substackcdn.com/image/fetch/$s_!cIpq!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4fd2d395-064e-40e8-b7c0-f2161f0d5a78_558x150.png)

1. Em “*Firewall → Rules*” vamos selecionar a interface que queremos configurar, neste caso **Amarelo1**;
2. Vamos adicionar uma nova Regra, selecionamos *Add* (neste caso, uma regra acima);
3. Preencheremos seguindo as seguintes configurações:

![](https://substackcdn.com/image/fetch/$s_!Z2kS!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F82d1b8c6-5ccd-4ac0-98a2-8eb3c2e7aba2_1140x577.png)

Devemos repetir o processo para as demais interfaces, respeitando suas subnets e configurações.

# **Testando nossas configurações**

Para testar nossas configurações, vamos pingar computadores da rede rosa a partir da rede amarela e vice-versa.

![](https://substackcdn.com/image/fetch/$s_!kUNR!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5679db04-3dc8-4104-955a-08ccda991283_797x817.png)

![](https://substackcdn.com/image/fetch/$s_!ZLER!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1a44dbfc-8e0f-450a-ba8e-686013255852_794x813.png)

# **Conclusão**

Neste laboratório, exploramos os passos para a configuração de um roteamento estático bem simples através do PfSense.

[Laboratório - Roteamento estático com PfSense](https://www.youtube.com/watch?v=pLsezKyGdpk)