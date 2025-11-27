📘 Sistema de Streaming / Assinaturas – Design Patterns em Python
1. Introdução

Este projeto implementa um sistema de assinatura de streaming utilizando padrões de projeto (Design Patterns) para garantir flexibilidade, extensibilidade e baixo acoplamento. Ele atende às exigências do trabalho acadêmico, utilizando os padrões:

Strategy – cálculo de pró-rata ao trocar de plano (upgrade/downgrade)

Decorator – adicionar recursos extras ao plano (4K, telas extras, downloads, etc.)

Observer – notificar usuário e sistema quando houver mudanças de plano ou cobranças

Factory Method – criação de estratégias conforme configuração

Singleton – configuração global e logger centralizado

O sistema possui um menu simples (CLI) exibindo “Desenvolvido por: Anderson Adriano Marchi” conforme solicitado.

2. Objetivo do Sistema

O objetivo é simular a lógica de assinatura de um serviço de streaming, permitindo:

criar uma assinatura;

trocar de plano com cálculo de pró-rata;

aplicar add-ons cumulativos via Decorator;

emitir notificações via Observer;

gerar logs centralizados;

manter uma arquitetura organizada e extensível.

3. Padrões Utilizados
✔ Strategy – Cálculo de Pró-Rata

Utilizado para calcular o valor proporcional quando o usuário muda de plano no meio do ciclo.

Implementações típicas:

UpgradeStrategy

DowngradeStrategy

NeutralStrategy (sem mudança)

Justificativa:

Facilita a troca dinâmica da regra de cálculo conforme o tipo de mudança, sem alterar a lógica principal do sistema.

✔ Decorator – Add-ons do Plano

Permite adicionar funções como:

4K (AddOn4KDecorator)

Telas extras (ExtraScreensDecorator)

Downloads offline, etc.

Justificativa:

Add-ons são opcionais, cumulativos e devem manter a interface comum do plano. O padrão Decorator evita uma explosão de subclasses e permite combinações flexíveis.

✔ Observer – Notificações

Qualquer mudança de plano ou cobrança dispara eventos que são enviados a observadores como:

EmailObserver

BillingObserver

WebhookObserver (exemplo)

Justificativa:

O sistema precisa reagir automaticamente a eventos sem acoplar regras de notificação à lógica principal.

✔ Factory Method – Criação de Estratégias

Remove condicionais do tipo if change == "upgrade" retornando a estratégia correta automaticamente.

Justificativa:

Centraliza criação de estratégias, permitindo incluir novas regras sem modificar código existente (Open/Closed Principle).

✔ Singleton – Configuração e Logger

A aplicação possui:

ConfigSingleton – tabela de tarifas/cenários

LoggerSingleton – registro de mensagens

Justificativa:

Configurações e logs precisam de instância única, garantindo consistência e evitando múltiplos carregamentos.

4. Estrutura de Pastas
design_patterns/
│
├── app/
│   └── cli.py
│
├── domain/
│   ├── inscricao.py
│   └── user.py
│
├── strategy/
│   ├── base.py
│   ├── desconto.py
│   ├── pro_rata.py
│   └── tarifa.py
│
├── decorators/
│   ├── adds.py
│
├── observer/
│   ├── ob_base.py
│   ├── email_ob.py
│   ├── billing_ob.py
│
├── factory/
│   └── strategy_factory.py
│
├── infra/
│   ├── log.py
│   └── singleton.py
│
└── teste/
    ├── test_strategy.py
    ├── test_decorator.py
    └── test_observer.py

5. Diagrama
Fluxo geral do sistema
flowchart TD
    A[Usuário] --> B[Menu CLI]
    B --> C[Assinatura]
    C --> D[Strategy - Cálculo Pró-Rata]
    C --> E[Decorator - Adds]
    C --> F[Observer - Notificações]
    D --> G[StrategyFactory]
    F --> H[EmailOb]
    F --> I[BillingOb]
    C --> J[Singleton / Logger]

6. Como Executar
1. Criar ambiente virtual (opcional)
python -m venv venv
source venv/bin/activate  # Linux
venv\Scripts\activate     # Windows

2. Rodar o menu principal
python app/cli.py

3. Rodar os testes
python -m unittest discover teste

7. Decisões de Design

Foi usada composição em vez de herança sempre que possível.

O sistema separa domínio, infraestrutura e padrões para maior clareza.

Add-ons foram isolados via Decorator para evitar subclasses desnecessárias.

Notificações foram desacopladas com Observer, permitindo adicionar novos canais facilmente.

Strategy foi colocado em fábrica para facilitar extensões futuras.

Configurações centralizadas via Singleton evitam múltiplas instâncias divergentes.

8. Limitações

O sistema não conecta a banco de dados (mockado).

Não há interface gráfica, apenas CLI.

Valores e cálculos são exemplos simplificados.

Notificações são simuladas (print/log), não enviadas realmente.

9. Créditos

Desenvolvido por: Anderson Adriano Marchi
