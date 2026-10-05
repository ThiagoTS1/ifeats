# IFeats

Aplicativo de delivery de comida para celular, feito em React Native com Expo. Um único app atende os quatro perfis da plataforma: cliente, restaurante, entregador e administrador. O back-end é a [sigeg-api](https://github.com/Juan-Souzaa/sigeg-api).

<p>
  <img src="https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React Native">
  <img src="https://img.shields.io/badge/Expo-000020?style=for-the-badge&logo=expo&logoColor=white" alt="Expo">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript">
  <img src="https://img.shields.io/badge/Jest-C21325?style=for-the-badge&logo=jest&logoColor=white" alt="Jest">
</p>

## Funcionalidades

**Cliente**

- Cadastro, login e edição de perfil
- Endereços com preenchimento automático pelo CEP (ViaCEP)
- Lista de restaurantes por categoria e cardápio
- Carrinho com cupom de desconto
- Checkout com pagamento em dinheiro, PIX ou cartão de crédito
- Acompanhamento do pedido e rastreamento da entrega no mapa
- Avaliação do pedido e abertura de tickets de suporte

**Restaurante**

- Cadastro do restaurante e edição do perfil
- Cardápio: cadastro e edição de pratos com foto
- Fila de pedidos e mudança de status
- Raio de entrega, avaliações recebidas e ganhos

**Entregador**

- Cadastro com localização
- Pedidos disponíveis, aceite e detalhe da entrega com rota no mapa
- Ganhos por entrega

**Administrador**

- Aprovação de restaurantes e entregadores pendentes
- Pedidos em andamento, reembolso e tickets
- Cupons, taxas da plataforma e relatórios

## Arquitetura

O app separa tela, lógica e acesso à API:

```
src/
├── screens/      Telas, só com layout e ligação com o hook
├── hooks/        Um ViewModel por tela (useXxxViewModel), com estado e regras
├── services/     Chamadas HTTP com axios, uma por recurso da API
├── context/      Autenticação e carrinho
├── navigation/   Um navegador por perfil, escolhido pelo papel no token
├── components/   Componentes de interface reutilizáveis
├── theme/        Cores e espaçamentos
├── types/        Tipos dos dados da API
└── utils/        Formatação, validação e leitura do JWT
```

O token JWT fica guardado com `expo-secure-store`, e o papel do usuário dentro dele decide qual navegador abre depois do login.

## Como rodar

Pré-requisitos: Node.js, o app Expo Go ou um emulador, e a [sigeg-api](https://github.com/Juan-Souzaa/sigeg-api) rodando.

```bash
git clone https://github.com/Juan-Souzaa/ifeats.git
cd ifeats
npm install
cp .env.example .env
npx expo start
```

No `.env`, aponte `EXPO_PUBLIC_API_BASE_URL` para a API:

| Onde o app roda | Valor |
|---|---|
| Emulador Android | `http://10.0.2.2:8080` |
| Celular ou simulador iOS na mesma rede | `http://IP_DO_COMPUTADOR:8080` |

## Testes

Os ViewModels e os utilitários têm testes com Jest:

```bash
npm test
npm run test:ci
```
