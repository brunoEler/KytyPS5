<div align="center">

# KYTYPS5
### ASTRO BOT · BUILD EXPERIMENTAL

Uma versão recente do emulador, com a correção de mip views portada para testes no Windows.

[![Windows x64](https://img.shields.io/badge/Windows-x64-38bdf8?style=for-the-badge&labelColor=0f172a)](https://github.com/brunoEler/KytyPS5/actions/workflows/build.yml)
[![Experimental](https://img.shields.io/badge/Build-Experimental-fbbf24?style=for-the-badge&labelColor=0f172a)](#antes-de-testar)
[![GPL 2.0](https://img.shields.io/badge/Licen%C3%A7a-GPL--2.0-a5b4fc?style=for-the-badge&labelColor=0f172a)](LICENSE)

**[BAIXAR COMPILAÇÃO](https://github.com/brunoEler/KytyPS5/actions/runs/44831252534)** &nbsp; · &nbsp; **[GERAR VERSÃO ATUALIZADA](https://github.com/brunoEler/KytyPS5/actions/workflows/astro-windows.yml)** &nbsp; · &nbsp; **[PROJETO ORIGINAL](https://github.com/KytyPS5/KytyPS5)**

</div>

---

## O que tem aqui

Este fork reúne o código do **KytyPS5** e uma adaptação da correção para o erro de textura encontrado no **ASTRO BOT**:

```text
unsupported texture mip view changes physical layout:
base=6 last=6 max=5
extent=1920x1080x1 tile=27
```

A correção tenta manter a mip view na cadeia declarada quando o layout físico permite, antes de recorrer a uma cadeia independente.

| Componente | Origem |
| :--- | :--- |
| Emulador e launcher | Projeto KytyPS5 |
| Correção original de mip views | Nawid3333 · PR #2172 |
| Base do primeiro porte | Upstream `a21fd80` · 20/11/2026 |
| Adaptação e configuração deste fork | ChatGPT / OpenAI Codex |
| Solicitação e propriedade deste fork | brunoEler |

## Baixar e testar

**[→ Abrir a compilação com a correção](https://github.com/brunoEler/KytyPS5/actions/runs/44831252534)**

1. Entre na sua conta do GitHub.
2. Confira se a etapa **Build KytyPS5 (Windows)** terminou com sucesso.
3. Na seção **Artifacts**, baixe **KytyPS5-Windows-x64**.
4. Extraia o ZIP em uma pasta nova.
5. Abra `kyty_launcher.exe` e configure o caminho dos seus arquivos do jogo.

> **O arquivo só aparece depois que a etapa Windows termina e publica o artefato.** O botão acima leva à compilação; não indica que o download já está pronto.

## Gerar uma versão mais recente

**[→ Abrir o fluxo Astro Bot — latest Windows with mip fix](https://github.com/brunoEler/KytyPS5/actions/workflows/astro-windows.yml)**

No GitHub Actions, clique em **Run workflow** e mantenha `upstream_ref` como `main` para usar o código mais recente do projeto original. Também é possível informar uma tag ou um commit.

O fluxo busca a revisão escolhida, tenta aplicar a adaptação e compila para Windows. **Se o trecho esperado tiver mudado, ele interrompe a execução para revisão manual.** Isso evita aplicar a alteração sem verificar o contexto.

Este fluxo é manual: não acompanha nem atualiza automaticamente cada lançamento.

## Antes de testar

| Verificação | Situação |
| :--- | :--- |
| Aplicação do patch ao código de `a21fd80` | Verificada localmente |
| Resultado da compilação | Consulte o GitHub Actions |
| Validação deste fork dentro do jogo | Ainda não realizada |
| Compatibilidade com próximas revisões | Depende da aplicação do patch e de novos testes |

Resolver este erro específico não garante que o jogo inteiro funcione. Resultados de testes publicados na PR original pertencem aos seus respectivos colaboradores e não validam automaticamente os binários deste fork.

<details>
<summary><strong>Detalhes técnicos da adaptação</strong></summary>

A alteração fica em:

```text
src/graphics/host_gpu/renderer/pipeline/descriptors.cpp
```

A função `MatchTextureMipView` contém a lógica de comparação dos layouts. `ResolveTextureMipView` guarda uma cópia da imagem declarada e tenta a resolução nessa cadeia antes do fallback que usa uma cadeia independente.

O porte preserva a comparação de mip layouts por igualdade presente na base mais recente. As mudanças de testes da PR original não foram portadas neste trabalho.

Referências:

- [PR #2172 — correção original](https://github.com/KytyPS5/KytyPS5/pull/2172)
- [Head da PR usado como referência: 81d29d43](https://github.com/Nawid3333/KytyPS5/commit/81d29d43cb151883949d5f0cfd3c1d1a3bf80e13)
- [Compilação de teste original da PR](https://github.com/KytyPS5/KytyPS5/actions/runs/43278578608)
- [Documentação original de compilação e uso](https://github.com/KytyPS5/KytyPS5/tree/a21fd80#building)

</details>

## Créditos e transparência

**KytyPS5** é desenvolvido pelos autores e colaboradores do [projeto original](https://github.com/KytyPS5/KytyPS5), com base no [Kyty de InoriRus](https://github.com/InoriRus/Kyty).

**Nawid3333 é o autor da correção original de mip views**, proposta na [PR #2172](https://github.com/KytyPS5/KytyPS5/pull/2172).

**ChatGPT / OpenAI Codex** realizou o porte dessa correção existente, configurou este fork, criou o fluxo de compilação com verificação do trecho e reformulou esta página, a pedido de **brunoEler**. Não se trata de uma correção descoberta independentemente pela IA.

**brunoEler é o solicitante e dono do fork, não o autor da correção ou das adaptações feitas pela IA.**

---

<div align="center">

**Fork experimental da comunidade · Sem vínculo com Sony ou PlayStation**

Não distribui jogos nem software de sistema protegido. Use arquivos de jogos obtidos legalmente.

[GPL-2.0-only](LICENSE) · [Licença original do Kyty](LICENSES/Kyty-MIT.txt) · Licenças de terceiros preservadas

</div>
