# CEP Barbacena

Landing page para consulta de endereços de Barbacena, MG, desenvolvida como atividade prática da disciplina de Programação 2 do 2º Período do curso de Bacharelado em Sistemas de Informação da UEMG, Unidade Acadêmica de Carangola. O design usa uma linguagem editorial sóbria, com a rosa como referência discreta à Cidade das Rosas.

## Funcionalidades

- Consulta direta de CEP com máscara `00000-000`.
- Busca de ruas, avenidas, praças e bairros por nome.
- Autocomplete a partir de 3 caracteres digitados.
- Sugestões reais da base consolidada, com navegação por mouse, `↑`, `↓`, `Enter` e `Esc`.
- Ao selecionar uma sugestão, o endereço completo é renderizado diretamente a partir da base local, sem nova consulta à API.
- Exibição de logradouro, bairro, cidade, UF e CEP.
- CEP em destaque visual de alto contraste no resultado.
- Link direto para visualizar o endereço completo no Google Maps.
- Rolagem suave automática até a seção de resultados.
- Aviso quando o CEP consultado pertence a outro município.
- Hero com foto licenciada da Basílica de São José Operário em Barbacena, publicada por ThiagoRuiz no Wikimedia Commons sob CC BY-SA 3.0.
- Logos do curso de Sistemas de Informação e da UEMG Carangola no header e footer.
- Modais acessíveis de Sobre (com transparência de IA), Termos de Uso e Privacidade.
- Estados de validação, carregamento, erro e resultado não encontrado.
- Interface responsiva, sem frameworks, com foco visível e suporte a `prefers-reduced-motion`.

## Equipe

- Emannuely Vanuzia da Silva Carlos
- Carlos Henrique Souza Costa
- Lavinya Sannliver Terra Soares

## Tecnologias

- HTML5 semântico
- CSS3 puro
- JavaScript Vanilla
- JSON local consolidado em `data/ceps.json`
- API ViaCEP para consulta de endereços em tempo real

## Executar localmente

Como o navegador bloqueia `fetch` de arquivos locais, sirva a pasta com qualquer servidor HTTP estático. Por exemplo:

```bash
python -m http.server 8000
```

Depois, acesse `http://localhost:8000`.

## Consultas e dados

`data/ceps.json` mantém 143 registros locais usados pelo autocomplete e pela busca reativa. Eles foram consolidados a partir dos três endpoints obrigatórios da ViaCEP:

- `https://viacep.com.br/ws/MG/Barbacena/Rua/json/` — 50 registros
- `https://viacep.com.br/ws/MG/Barbacena/Avenida/json/` — 43 registros
- `https://viacep.com.br/ws/MG/Barbacena/Praca/json/` — 50 registros

O campo de CEP consulta em tempo real:

```text
https://viacep.com.br/ws/{CEP}/json/
```

A busca por rua, avenida ou praça consulta:

```text
https://viacep.com.br/ws/MG/Barbacena/{logradouro}/json/
```

O autocomplete utiliza `data/ceps.json` e apresenta o endereço completo imediatamente ao selecionar uma sugestão. A busca enviada pelo formulário consulta a ViaCEP por logradouro e, quando não encontra resultados, pesquisa o termo na base local consolidada. A base local também é usada para manter o autocomplete funcional sem depender da API.

## Estrutura

```text
.
├── index.html
├── styles.css
├── script.js
├── data/
│   └── ceps.json
├── assets/
│   ├── basilica-sao-jose.jpg
│   ├── logo_uemg.png
│   └── logosis03.png
└── scripts/
    └── atualizar-ceps.js
```

O script `scripts/atualizar-ceps.js` refaz as consultas de Rua, Avenida e Praça e atualiza o arquivo consolidado local. Execute-o a partir da raiz do projeto com Node.js:

```bash
node scripts/atualizar-ceps.js
```

#sistemasuemgcarangola2p20262

