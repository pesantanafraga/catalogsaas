# PROJECT_NAME
## MASTER DEVELOPMENT SPECIFICATION
### Plataforma Modular de Catálogos Digitais

**Versão:** 1.0.0  
**Status:** Especificação aprovada para desenvolvimento  
**Nome comercial:** A definir  
**Identificador técnico:** PROJECT_NAME  
**Idioma inicial:** Português brasileiro (pt-BR)  
**Arquitetura:** Modular Monolith  
**Backend:** PHP + Laravel  
**Frontend administrativo:** Vue 3 + TypeScript  
**Construtor visual:** Desenvolvimento nativo  
**Banco de dados:** MySQL  
**Distribuição:** Self-hosted + SaaS  
**Comercialização:** Licenças perpétuas + assinaturas  

---

# 1. MISSÃO DO PROJETO

Desenvolver uma plataforma profissional, modular, escalável e comercializável para criação e gerenciamento de catálogos digitais personalizados.

O sistema deverá permitir que qualquer empresa crie seu próprio catálogo online sem conhecimentos de programação.

Durante a instalação ou criação de uma conta, o usuário selecionará o segmento empresarial desejado.

A plataforma deverá preparar automaticamente:

- Estrutura administrativa.
- Banco de dados.
- Módulos específicos.
- Campos personalizados.
- Categorias.
- Componentes visuais.
- Templates.
- Páginas iniciais.
- Configurações padrão.
- Funcionalidades específicas do segmento.

O projeto deverá funcionar em duas modalidades:

**SELF-HOSTED:** instalação individual em hospedagens ou servidores dos clientes.

**SAAS:** plataforma centralizada, com múltiplos clientes, cada um possuindo seu próprio ambiente administrativo e catálogo.

O objetivo não é criar diferentes sistemas independentes, mas uma única plataforma capaz de atender diferentes segmentos por meio de módulos extensíveis.

# 2. REGRAS FUNDAMENTAIS DO DESENVOLVIMENTO

Estas regras são obrigatórias e deverão ser respeitadas durante todo o projeto.

1. Não desenvolver o sistema inteiro em uma única etapa.
2. Não criar funcionalidades fictícias ou botões sem implementação.
3. Não substituir funcionalidades reais por dados simulados na versão de produção.
4. Não duplicar código quando uma funcionalidade puder pertencer ao Core.
5. Não permitir que módulos alterem diretamente componentes internos do Core sem contratos definidos.
6. Não misturar funcionalidades específicas de segmentos diferentes.
7. Não armazenar HTML ou JavaScript arbitrário de clientes no Builder.
8. Não comprometer o isolamento de dados entre clientes SaaS.
9. Não implementar recursos sem testes correspondentes.
10. Não avançar de fase enquanto os critérios de aceitação da fase atual não forem cumpridos.
11. Manter documentação técnica atualizada.
12. Priorizar compatibilidade com hospedagens PHP convencionais, dentro dos requisitos documentados.
13. Evitar dependências desnecessárias.
14. Não introduzir microsserviços na primeira arquitetura.
15. Não remover funcionalidades existentes para simplificar novas implementações.

Sempre que uma decisão arquitetural importante precisar ser alterada, registrar a justificativa no documento ADR (Architecture Decision Records).

# 3. STACK TECNOLÓGICA

Utilizar versões estáveis e compatíveis entre si, verificando os requisitos oficiais das dependências antes da instalação.

## Backend

- PHP 8.3 ou superior, conforme compatibilidade da versão escolhida do Laravel.
- Laravel.
- Composer.
- Eloquent ORM.
- Laravel Migrations.
- Laravel Policies.
- Laravel Events.
- Laravel Queues.
- Laravel Scheduler.
- Laravel Validation.

## Frontend administrativo

- Vue 3.
- TypeScript.
- Vite.
- Pinia.
- Vue Router, quando necessário.
- CSS moderno.
- Biblioteca de ícones Lucide.
- Biblioteca de drag and drop compatível com Vue 3.

## Comunicação

- REST API.
- JSON.
- Fetch API ou Axios.
- Webhooks.
- HTTPS obrigatório em produção.

## Banco de dados

- MySQL 8 ou superior.
- Índices adequados.
- Foreign Keys.
- Migrations versionadas.
- Transações.
- Estratégia de backup e restauração.

## Infraestrutura

- Linux.
- Nginx ou Apache.
- PHP-FPM.
- Redis opcional.
- Supervisor opcional.
- Docker para desenvolvimento e implantação em VPS.

O sistema deverá continuar funcional em instalações sem Redis, filas permanentes ou serviços adicionais, utilizando alternativas compatíveis com hospedagem compartilhada quando necessário.

# 4. ARQUITETURA DO SISTEMA

Adotar arquitetura de Monólito Modular.

Separar as responsabilidades em:

1. Core.
2. Authentication.
3. Administration.
4. Modules.
5. Themes.
6. Visual Builder.
7. Media Management.
8. Public Frontend.
9. Licensing.
10. Subscription Management.
11. SaaS Management.
12. API.

## 4.1 Core

O Core será responsável por:

- Inicialização da aplicação.
- Configurações.
- Autenticação.
- Autorização.
- Usuários.
- Empresas.
- Tenants.
- Banco de dados.
- Registro de módulos.
- Eventos.
- Logs.
- Segurança.
- Atualizações.
- Sistema de extensões.
- Serviços compartilhados.

O Core não poderá possuir dependências de funcionalidades específicas de restaurante, concessionária ou outros segmentos.

## 4.2 Sistema de módulos

Criar um mecanismo de descoberta e registro de módulos.

Cada módulo deverá possuir:

- Identificador.
- Nome.
- Descrição.
- Versão.
- Requisitos.
- Migrations.
- Models.
- Controllers.
- Services.
- Routes.
- Permissions.
- Settings.
- Components.
- Widgets.
- Templates.
- Resources.
- Testes.

Cada módulo deverá possuir um manifesto module.json validado.

O registro de módulos deverá permitir:

- Instalar.
- Ativar.
- Desativar.
- Atualizar.
- Consultar dependências.
- Verificar compatibilidade.
- Registrar permissões.

A desativação de um módulo não deverá excluir automaticamente os dados armazenados.

A remoção de dados deverá ser uma operação separada, com confirmação e backup.

## 4.3 Contratos dos módulos

Criar interfaces padronizadas para:

- ModuleInterface.
- ModuleServiceProvider.
- ModuleInstallerInterface.
- ModuleMigrationInterface.
- ComponentInterface.
- WidgetInterface.
- ThemeInterface.

Não permitir que os módulos dependam de implementação interna não documentada do Core.

# 5. ESTRUTURA DE DIRETÓRIOS

Utilizar a estrutura padrão do Laravel e organizar os domínios sem duplicar diretórios fundamentais.

Estrutura lógica pretendida:

PROJECT_NAME/

├── app/
│   ├── Core/
│   │   ├── Contracts/
│   │   ├── Services/
│   │   ├── Events/
│   │   ├── Exceptions/
│   │   └── Support/
│   │
│   ├── Http/
│   │   ├── Controllers/
│   │   ├── Middleware/
│   │   └── Requests/
│   │
│   ├── Models/
│   ├── Policies/
│   └── Providers/
│
├── Modules/
│   ├── Restaurant/
│   ├── Automotive/
│   ├── RealEstate/
│   ├── Fashion/
│   └── Supermarket/
│
├── Builder/
│   ├── Components/
│   ├── Schemas/
│   ├── Renderers/
│   ├── Validators/
│   └── Services/
│
├── Themes/
│   ├── Shared/
│   ├── Restaurant/
│   └── Automotive/
│
├── resources/
│   ├── js/
│   │   ├── admin/
│   │   ├── builder/
│   │   ├── components/
│   │   ├── composables/
│   │   ├── stores/
│   │   └── types/
│   │
│   ├── css/
│   ├── views/
│   └── lang/
│       └── pt_BR/
│
├── database/
│   ├── migrations/
│   ├── seeders/
│   └── factories/
│
├── routes/
│   ├── web.php
│   ├── api.php
│   └── admin.php
│
├── public/
├── storage/
├── tests/
│   ├── Unit/
│   ├── Feature/
│   ├── Integration/
│   └── Browser/
│
├── docs/
│   ├── ARCHITECTURE.md
│   ├── DATABASE.md
│   ├── MODULES.md
│   ├── BUILDER.md
│   ├── INSTALLER.md
│   ├── SAAS.md
│   ├── LICENSING.md
│   ├── SECURITY.md
│   ├── API.md
│   ├── ROADMAP.md
│   ├── ADR/
│   └── CHANGELOG.md
│
├── install/
├── artisan
├── composer.json
├── package.json
└── README.md

A estrutura deverá respeitar as convenções do Laravel e utilizar autoload PSR-4 para os módulos.

# 6. SISTEMA MULTI-TENANT

Desenvolver uma arquitetura que permita múltiplas empresas utilizando a mesma instalação SaaS.

Cada tenant deverá possuir:

- Identificador único.
- Nome empresarial.
- Slug.
- Domínios.
- Configurações.
- Usuários.
- Módulos.
- Plano comercial.
- Limites.
- Arquivos.
- Páginas.
- Catálogo.

## Estratégia inicial

Banco compartilhado com isolamento lógico por tenant_id.

Todas as entidades pertencentes a clientes deverão respeitar o contexto do tenant.

Criar middleware responsável por identificar o tenant a partir do domínio ou subdomínio.

Implementar mecanismos de proteção para evitar acesso cruzado.

O tenant deverá ser validado no servidor. Nunca confiar apenas no identificador recebido pelo frontend.

Criar testes automatizados comprovando que um cliente não consegue visualizar, editar ou excluir dados de outro cliente.

## Self-hosted

Cada instalação individual deverá operar com seu próprio banco de dados e arquivos.

A aplicação deverá utilizar uma estrutura compatível com o modelo multi-tenant, mesmo quando existir apenas um tenant.

# 7. INSTALADOR INTELIGENTE

Desenvolver um assistente de instalação com interface moderna e responsiva.

## Etapas

1. Verificação do ambiente.
2. Verificação da versão PHP.
3. Verificação das extensões necessárias.
4. Verificação de permissões.
5. Configuração do banco.
6. Teste de conexão.
7. Dados da empresa.
8. Criação do administrador.
9. Seleção do segmento.
10. Seleção do template.
11. Identidade visual inicial.
12. Instalação dos módulos.
13. Execução das migrations.
14. Criação dos dados iniciais.
15. Finalização.

## Segmentos iniciais

- Restaurante.
- Automotivo.

Outros segmentos deverão aparecer somente quando estiverem efetivamente disponíveis para instalação.

## Requisitos

- Instalação limpa.
- Controle de etapas concluídas.
- Tratamento de erros.
- Possibilidade de retomar etapas seguras.
- Registro de logs.
- Proteção contra execução duplicada.
- Bloqueio definitivo após instalação.
- Proteção contra acesso direto ao instalador após conclusão.

Nunca executar SQL arbitrário enviado por módulos.

Utilizar migrations e instaladores registrados e validados.

# 8. MODELO DE DADOS

Desenvolver migrations e relacionamentos para os seguintes grupos.

## Core

- users
- roles
- permissions
- role_permissions
- settings
- audit_logs
- system_logs

## Multi-tenancy

- tenants
- tenant_domains
- tenant_users
- tenant_settings
- tenant_modules
- tenant_usage

## Catálogo

- categories
- products
- product_images
- product_variants
- product_attributes
- product_attribute_values
- product_category

## Conteúdo

- pages
- page_versions
- page_publications
- menus
- menu_items
- media
- media_folders

## Temas

- themes
- theme_settings
- theme_assets
- design_tokens

## Builder

- builder_components
- builder_templates
- page_builder_data

## Comercial

- plans
- subscriptions
- licenses
- license_activations
- payments
- invoices
- coupons
- feature_limits
- webhooks

Os módulos específicos deverão criar suas próprias tabelas.

Não criar tabelas de todos os segmentos antecipadamente.

Utilizar migrations independentes e versionadas.

Todos os dados deverão possuir tipos adequados, relacionamentos, índices e regras de integridade.

# 9. MÓDULO RESTAURANTE

Desenvolver o primeiro módulo de negócio.

## Funcionalidades administrativas

- Cadastro de pratos.
- Categorias.
- Descrição.
- Preços.
- Imagens.
- Ingredientes.
- Adicionais.
- Tamanhos.
- Disponibilidade.
- Destaques.
- Promoções.
- Horários de funcionamento.
- Informações comerciais.

## Frontend

- Cardápio digital.
- Categorias.
- Busca.
- Filtros.
- Detalhes do prato.
- Galeria.
- Preços.
- Botão de WhatsApp.
- Informações de contato.
- Horários.

## Preparação para futuras versões

- Pedidos.
- Carrinho.
- Delivery.
- Retirada.
- Mesas.
- Pagamentos.
- Gestão de pedidos.

Essas funcionalidades transacionais não deverão ser simuladas na primeira versão.

# 10. MÓDULO AUTOMOTIVO

Desenvolver o segundo módulo.

## Funcionalidades administrativas

- Cadastro de veículos.
- Marcas.
- Modelos.
- Ano de fabricação.
- Ano do modelo.
- Quilometragem.
- Combustível.
- Câmbio.
- Cor.
- Portas.
- Preço.
- Descrição.
- Opcionais.
- Galeria de imagens.
- Disponibilidade.

## Frontend

- Vitrine de veículos.
- Busca.
- Filtros.
- Página individual do veículo.
- Galeria.
- Informações técnicas.
- Veículos relacionados.
- Formulário de interesse.
- Botão de WhatsApp.

## Preparação futura

- Simulação de financiamento.
- Avaliação de usados.
- Agendamento de test drive.
- Integração com estoque externo.

# 11. SISTEMA DE TEMAS

Desenvolver uma estrutura independente do conteúdo.

Cada tema deverá possuir:

- Manifesto.
- Identificador.
- Nome.
- Segmento compatível.
- Versão.
- Preview.
- Layout.
- Header.
- Footer.
- Componentes.
- Assets.
- Design tokens.

Permitir instalação e seleção de temas.

O usuário deverá conseguir trocar de tema sem perder produtos, categorias, páginas ou arquivos.

A troca deverá preservar os dados e permitir revisar os componentes incompatíveis antes da publicação.

# 12. SISTEMA DE PERSONALIZAÇÃO

Desenvolver uma interface administrativa para configurar:

- Logotipo.
- Favicon.
- Cores.
- Tipografia.
- Botões.
- Fundos.
- Bordas.
- Sombras.
- Cabeçalho.
- Rodapé.
- Largura de conteúdo.
- Redes sociais.
- Informações comerciais.

Utilizar CSS Variables e design tokens.

Permitir pré-visualização antes de publicar.

# 13. GERENCIADOR DE MÍDIA

Desenvolver biblioteca de mídia independente.

Funcionalidades:

- Upload múltiplo.
- Pastas.
- Categorias.
- Busca.
- Filtros.
- Preview.
- Dimensões.
- Tamanho do arquivo.
- Texto alternativo.
- Recorte.
- Compressão.
- WebP.
- AVIF quando suportado.
- Miniaturas.
- Exclusão controlada.

## Recomendações de dimensões iniciais

- Banner desktop: 1920 × 600 px.
- Banner mobile: 750 × 900 px.
- Banner intermediário: 1200 × 400 px.
- Produto: 1000 × 1000 px.
- Categoria: 600 × 600 px.
- Logo: 500 × 200 px.

As dimensões deverão ser configuráveis por tema e componente.

O sistema deverá informar as dimensões recomendadas durante o upload.

Validar MIME real, extensão, tamanho e conteúdo dos arquivos.

Nunca permitir execução de arquivos enviados.

# 14. VISUAL BUILDER NATIVO

Desenvolver um construtor visual próprio utilizando Vue 3 e TypeScript, integrado ao Laravel.

Não utilizar o Elementor ou outro construtor de páginas como dependência central.

## Estrutura visual

O editor deverá possuir:

1. Barra superior.
2. Biblioteca de componentes.
3. Canvas.
4. Painel de propriedades.
5. Alternância de dispositivos.
6. Histórico.
7. Salvamento.
8. Preview.
9. Publicação.

## Componentes universais

- Container.
- Seção.
- Colunas.
- Título.
- Texto.
- Imagem.
- Banner.
- Botão.
- Ícone.
- Galeria.
- Vídeo.
- Divisor.
- Espaçamento.
- Links.
- Redes sociais.
- Mapa.
- Formulário.

## Componentes específicos

Restaurante:
- Cardápio.
- Prato.
- Categorias.
- Prato em destaque.
- Promoções.
- Horários.

Automotivo:
- Veículos.
- Veículo em destaque.
- Marcas.
- Filtros.
- Ficha técnica.
- Veículos relacionados.

## Funcionalidades obrigatórias

- Drag and drop.
- Reordenação.
- Duplicação.
- Exclusão.
- Edição de propriedades.
- Edição de textos.
- Seleção de imagens.
- Controle de espaçamento.
- Controle de largura.
- Controle de altura.
- Cores.
- Bordas.
- Tipografia.
- Alinhamento.
- Responsividade.
- Visibilidade por dispositivo.
- Preview.
- Autosave.
- Rascunhos.
- Publicação.
- Histórico de versões.
- Restauração.

## Arquitetura dos componentes

Cada componente deverá possuir:

- Identificador.
- Nome.
- Tipo.
- Categoria.
- Ícone.
- Schema de propriedades.
- Valores padrão.
- Regras de validação.
- Renderer.
- Compatibilidade com dispositivos.

O registro de componentes deverá permitir que módulos registrem componentes próprios.

## Persistência

Armazenar a estrutura das páginas em JSON validado.

Não armazenar código PHP ou JavaScript arbitrário.

Implementar:

- Versionamento do schema.
- Validação no servidor.
- Validação no frontend.
- Migração de versões.
- Histórico.
- Preview.
- Publicação.

O renderer público deverá utilizar componentes autorizados e dados sanitizados.

O editor não poderá depender do frontend administrativo para renderizar páginas publicadas.

# 15. RESPONSIVIDADE

O sistema deverá adotar abordagem mobile-first.

Breakpoints iniciais:

- Mobile: até 767 px.
- Tablet: 768–1023 px.
- Desktop: 1024 px ou superior.

Permitir ajustes específicos por dispositivo.

Garantir que os componentes não provoquem overflow horizontal.

Testar em navegadores modernos.

O frontend deverá possuir layout responsivo mesmo quando o cliente não fizer nenhuma personalização.

# 16. FRONTEND PÚBLICO

Desenvolver sistema de renderização de catálogos.

Funcionalidades comuns:

- Header.
- Footer.
- Menu.
- Banner.
- Páginas.
- Catálogo.
- Categorias.
- Busca.
- Detalhes.
- Contato.
- WhatsApp.
- Redes sociais.

## SEO

- URLs amigáveis.
- Meta title.
- Meta description.
- Open Graph.
- Sitemap.
- Robots.txt.
- Canonical.
- Schema.org adequado ao segmento.

## Performance

- Lazy loading.
- WebP.
- AVIF quando suportado.
- Cache.
- Consultas otimizadas.
- Paginação.
- Assets compilados.
- CSS e JS otimizados.

# 17. SISTEMA COMERCIAL

Desenvolver infraestrutura preparada para:

## Licenças perpétuas

- Criação.
- Ativação.
- Validação.
- Domínios autorizados.
- Limites de instalação.
- Atualizações conforme contrato.
- Renovação opcional de serviços.

## Assinaturas

- Mensal.
- Anual.
- Planos.
- Limites.
- Recursos.
- Pagamentos.
- Cancelamento.
- Suspensão.
- Reativação.

## Painel proprietário

Desenvolver área administrativa independente para o proprietário da plataforma.

Funcionalidades:

- Clientes.
- Instalações.
- Licenças.
- Ativações.
- Planos.
- Assinaturas.
- Pagamentos.
- Módulos.
- Versões.
- Atualizações.
- Logs.
- Indicadores comerciais.

## Servidor de licenciamento

Desenvolver API centralizada.

Endpoints conceituais:

POST /api/licenses/activate

POST /api/licenses/validate

POST /api/licenses/deactivate

GET /api/licenses/updates

A comunicação deverá utilizar HTTPS e mecanismos de assinatura e autenticação.

Implementar cache local e período de tolerância para indisponibilidade temporária do servidor.

Nunca apagar os dados do cliente por inadimplência ou falha de validação.

# 18. API

Criar API REST versionada.

Prefixo:

/api/v1/

Endpoints gerais:

- /auth
- /pages
- /categories
- /products
- /media
- /settings
- /themes

Endpoints de segmentos:

- /restaurant/dishes
- /restaurant/categories
- /automotive/vehicles
- /automotive/brands

Implementar autenticação, autorização, validação, paginação, tratamento de erros e documentação.

Utilizar respostas padronizadas.

Preparar documentação OpenAPI.

# 19. SEGURANÇA

Implementar obrigatoriamente:

- Hash de senhas seguro.
- CSRF.
- Proteção XSS.
- Proteção SQL Injection.
- Validação de entrada.
- Escape de saída.
- Controle de permissões.
- Controle de sessões.
- Rate limiting.
- HTTPS.
- Proteção de uploads.
- Logs de auditoria.
- Isolamento SaaS.
- Backups.
- Proteção de arquivos privados.
- Autenticação de dois fatores para administradores.

O Builder deverá aceitar somente componentes registrados e propriedades validadas.

Não permitir execução de código arbitrário por clientes.

Documentar requisitos LGPD, exportação, retenção e exclusão de dados.

# 20. INTERNACIONALIZAÇÃO

O idioma inicial será português brasileiro.

Entretanto, todas as mensagens, menus, notificações, validações e textos do sistema deverão utilizar arquivos de tradução.

Não espalhar textos de interface diretamente pelo código.

Preparar suporte futuro para:

- Português brasileiro.
- Inglês.
- Espanhol.

Utilizar configuração adequada de moeda, data, horário e fuso horário por tenant.

# 21. TESTES

Utilizar PHPUnit ou Pest para testes PHP.

Utilizar testes de navegador com Playwright quando necessário.

Criar testes para:

- Instalação.
- Autenticação.
- Permissões.
- Módulos.
- Banco.
- Catálogo.
- Builder.
- Renderização.
- Responsividade.
- Upload.
- SaaS.
- Licenciamento.
- Assinaturas.
- API.
- Segurança.

Nenhuma funcionalidade crítica deverá ser considerada concluída sem testes.

# 22. FASES DE DESENVOLVIMENTO

O desenvolvimento deverá ocorrer na seguinte ordem.

## FASE 0 — PLANEJAMENTO E FUNDAÇÃO

Objetivos:

- Validar ambiente.
- Criar repositório.
- Criar Laravel.
- Configurar Composer.
- Configurar Vite.
- Configurar Vue.
- Configurar TypeScript.
- Configurar MySQL.
- Criar estrutura modular.
- Criar documentação.
- Criar ambiente de testes.

Entregáveis:

- Aplicação inicial executável.
- Estrutura de diretórios.
- README.
- ARCHITECTURE.md.
- ADR inicial.
- Ambiente de desenvolvimento documentado.

Critérios de aceitação:

- Aplicação executa sem erros.
- Banco conecta corretamente.
- Frontend compila.
- Testes iniciais executam.
- Estrutura documentada.

## FASE 1 — CORE E AUTENTICAÇÃO

Objetivos:

- Autenticação.
- Usuários.
- Roles.
- Permissions.
- Settings.
- Logs.
- Policies.
- Estrutura multi-tenant inicial.
- Registro de módulos.

Critérios de aceitação:

- Login funcional.
- Logout funcional.
- Controle de acesso.
- Permissões verificadas no servidor.
- Dados protegidos.
- Testes aprovados.

## FASE 2 — INSTALADOR

Objetivos:

- Assistente visual.
- Verificação do servidor.
- Configuração do banco.
- Criação do administrador.
- Seleção de segmento.
- Instalação de módulos.
- Migrations.
- Bloqueio de instalação concluída.

Critérios de aceitação:

- Instalação limpa funcional.
- Erros tratados.
- Instalação não pode ser repetida indevidamente.
- Segmento selecionado registrado.
- Módulos instalados corretamente.

## FASE 3 — SISTEMA MODULAR

Objetivos:

- Manifestos.
- Descoberta.
- Registro.
- Ativação.
- Desativação.
- Migrations específicas.
- Permissões.
- Eventos.
- Contratos.

Critérios de aceitação:

- Módulos independentes.
- Core não depende dos segmentos.
- Módulo pode ser instalado e ativado.
- Dependências verificadas.
- Dados preservados na desativação.

## FASE 4 — CATÁLOGO RESTAURANTE

Objetivos:

- Pratos.
- Categorias.
- Imagens.
- Adicionais.
- Tamanhos.
- Preços.
- Disponibilidade.
- Frontend público.

Critérios de aceitação:

- Cadastro e edição.
- Exclusão controlada.
- Categorias funcionais.
- Imagens funcionais.
- Catálogo público responsivo.
- WhatsApp funcional.

## FASE 5 — CATÁLOGO AUTOMOTIVO

Objetivos:

- Veículos.
- Marcas.
- Modelos.
- Especificações.
- Galeria.
- Filtros.
- Formulário de interesse.

Critérios de aceitação:

- Cadastro de veículos.
- Filtros funcionais.
- Página individual.
- Galeria.
- Formulário.
- Frontend responsivo.

## FASE 6 — TEMAS E PERSONALIZAÇÃO

Objetivos:

- Temas.
- Identidade visual.
- Cores.
- Tipografia.
- Header.
- Footer.
- Biblioteca de mídia.
- Banners.
- Preview.

Critérios de aceitação:

- Upload validado.
- Dimensões identificadas.
- Preview funcional.
- Temas independentes.
- Troca de tema sem perda de conteúdo.

## FASE 7 — VISUAL BUILDER

Objetivos:

- Interface Vue.
- Canvas.
- Componentes.
- Drag and drop.
- Propriedades.
- Responsividade.
- Autosave.
- Histórico.
- Preview.
- Publicação.

Critérios de aceitação:

- Inserção de componentes.
- Reordenação.
- Duplicação.
- Edição.
- Exclusão.
- Persistência JSON.
- Validação no servidor.
- Renderização pública.
- Histórico restaurável.
- Testes em diferentes dispositivos.

## FASE 8 — SAAS

Objetivos:

- Multi-tenancy completo.
- Domínios.
- Subdomínios.
- Isolamento.
- Provisionamento.
- Limites.
- Painel central.

Critérios de aceitação:

- Criação de tenant.
- Provisionamento automatizado.
- Isolamento validado por testes.
- Domínios funcionais.
- Limites respeitados.

## FASE 9 — LICENÇAS E ASSINATURAS

Objetivos:

- Servidor central.
- Licenças.
- Ativações.
- Planos.
- Assinaturas.
- Pagamentos.
- Webhooks.
- Atualizações.

Critérios de aceitação:

- Licença pode ser ativada.
- Validação funcional.
- Assinatura controlada.
- Webhooks autenticados e idempotentes.
- Falhas tratadas.
- Período de tolerância implementado.

## FASE 10 — ESTABILIZAÇÃO E LANÇAMENTO

Objetivos:

- Auditoria.
- Performance.
- Segurança.
- Documentação.
- Backups.
- Empacotamento.
- Atualizações.
- Implantação.

Critérios de aceitação:

- Testes críticos aprovados.
- Instalação self-hosted documentada.
- SaaS operacional.
- Backup e restauração testados.
- Pacote de distribuição validado.
- Documentação de operação concluída.

# 23. PADRÃO DE ENTREGA DE CADA FASE

Para cada fase, o agente deverá:

1. Ler a documentação existente.
2. Verificar o estado atual do repositório.
3. Identificar dependências.
4. Apresentar o plano de implementação.
5. Implementar as funcionalidades.
6. Criar migrations.
7. Criar testes.
8. Executar os testes.
9. Corrigir os erros.
10. Atualizar a documentação.
11. Atualizar o changelog.
12. Apresentar relatório de conclusão.

O relatório deverá conter:

- Funcionalidades implementadas.
- Arquivos criados.
- Arquivos modificados.
- Migrations.
- Testes executados.
- Resultado dos testes.
- Problemas conhecidos.
- Dependências adicionadas.
- Próxima etapa recomendada.

Não afirmar que uma funcionalidade foi implementada se apenas a interface visual tiver sido criada.

Não afirmar que os testes passaram sem executá-los.

# 24. PADRÃO DE QUALIDADE

O código deverá seguir:

- PSR-4.
- PSR-12.
- SOLID.
- DRY.
- KISS.
- Separação de responsabilidades.
- Tipagem sempre que possível.
- Nomenclatura consistente.
- Tratamento de exceções.
- Testes automatizados.
- Documentação.

Evitar:

- Controllers gigantes.
- Regras de negócio dentro das Views.
- SQL espalhado.
- Dependências circulares.
- Componentes duplicados.
- Arquivos monolíticos.
- Configurações hardcoded.
- Código inseguro.
- Funcionalidades simuladas em produção.

# 25. ROADMAP DE EXPANSÃO

Após a versão inicial:

- Imobiliárias.
- Moda.
- Supermercados.
- Eletrônicos.
- Catálogos de serviços.
- Extensões.
- Marketplace de templates.
- Marketplace de módulos.
- Aplicativo mobile.
- Integrações externas.
- Importação por planilhas.
- Integrações com CRM.
- Recursos avançados de analytics.

# 26. DIRETRIZ FINAL AO AGENTE DE DESENVOLVIMENTO

Você será responsável por atuar como arquiteto de software, desenvolvedor backend, desenvolvedor frontend, engenheiro de testes e responsável pela documentação técnica deste projeto.

Sua missão é transformar esta especificação em uma aplicação real, funcional, segura e comercializável.

Não tente desenvolver todas as fases de uma vez.

Comece analisando esta documentação e propondo a implementação da FASE 0.

Antes de escrever o código:

1. Explique a estrutura técnica proposta.
2. Identifique possíveis conflitos e lacunas.
3. Confirme a compatibilidade das dependências.
4. Apresente a estrutura inicial de arquivos.
5. Apresente o plano de execução.
6. Identifique os critérios de conclusão.

Após a aprovação do planejamento, execute a fase.

Trabalhe sempre com o código real do projeto, mantendo consistência entre arquivos, banco de dados, APIs, componentes e documentação.

Não simplifique funcionalidades essenciais sem autorização.

Quando encontrar uma limitação técnica, apresente alternativas e explique suas consequências antes de alterar a arquitetura.

Não avance automaticamente para outra fase se houver critérios de aceitação pendentes.

A prioridade é construir uma fundação extremamente sólida para que a plataforma possa evoluir durante anos, receber novos segmentos, suportar milhares de empresas e permitir que terceiros desenvolvam módulos e extensões.

**O resultado esperado não é um protótipo visual, mas um software profissional, funcional, extensível e pronto para evoluir comercialmente.**

---

# FIM DA ESPECIFICAÇÃO MESTRE