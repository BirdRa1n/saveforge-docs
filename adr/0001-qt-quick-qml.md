# ADR 0001 — Qt Quick/QML para a UI do Desktop

**Status:** Proposta · **Data:** 2026-11-09

## Contexto
A UI principal é uma biblioteca visual, com grade de capas, filtros, detalhes e histórico. O template atual do repositório usa Qt Widgets.

## Decisão
A interface será feita com **Qt Quick + Qt Quick Controls (QML)**. Todo o domínio fica em bibliotecas C++ sem dependência de QtGui ou QtQuick. A UI consome view models (`QAbstractListModel`, `QML_ELEMENT`) e chama a camada `services`.

## Consequências
- (+) Grades, animações, temas claro e escuro e escalonamento em DPI alto são naturais em QML.
- (+) O núcleo fica testável e pode ser reutilizado pela CLI.
- (−) Há uma curva de aprendizado de QML. Os diálogos nativos de arquivo vêm de `QtQuick.Dialogs`.
- O template Widgets atual será substituído na tarefa D0.1.

## Alternativas
- **Qt Widgets:** é maduro e nativo, mas uma biblioteca visual exigiria muitos delegates customizados.
- **Híbrido Widgets + QQuickWidget:** seriam dois paradigmas para manter. Rejeitado.
