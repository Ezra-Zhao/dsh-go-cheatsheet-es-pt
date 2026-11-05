# dsh-Go 速查表 | dsh-Go Cheatsheet | Guía rápida de dsh-Go

> 一页看懂 dsh-Go：DeepSeek Harness（dsh）的社区安卓客户端——把编程 agent 装进口袋。手机本机直接跑 dsh（App 内装 Ubuntu 与 Node.js 运行环境，免 root、免 Termux），也能经 SSH 或 DSH Remote 遥控你电脑上的 dsh，接着同一段对话干活。离开工位时拿它接着盯 agent、批审批、排排队，电脑可以关，agent 的活别停。

- 上游项目：[ccch1mneyyy/dsh-Go](https://github.com/ccch1mneyyy/dsh-Go)（2026-11-05 实测 11,277 ★ / 513 forks，AGPL-3.0；根目录只有简体中文 README 与 README.en.md，无西/葡语版）
- 平台：Android 8.0（API 26）及以上的手机或平板；现为 APK 侧载，不是 Google Play 发布配置
- 本页结构：中文主文 → English → Español → Português

---

Apoyo y más: [GitHub Sponsors](https://github.com/sponsors/Ezra-Zhao) · [Gumroad — plantillas y cuadernos que uso](https://ezraflow28.gumroad.com)

## 两种用法先选哪条路

| 路 | 怎么做 | 适合谁 |
|---|---|---|
| 本机跑 | 首启选「在本机安装运行环境」，App 内装 Ubuntu、Node.js 与 DSH，预留约 1 GB 空间；免 root、免 Termux | 手边没电脑、想随时开新对话的人 |
| 只遥控 | 手机不装运行环境，经 SSH 或 DSH Remote 连电脑/服务器上的 dsh，接着同一段对话干活 | 新手与低内存机先走这条；电脑上有现成环境的人 |

两条路都能切换模型、发图片、用语音输入、处理工具审批和提问，也都有原生界面与网页版可一键切换；回复中途能插话、能排队发「立即发送」。差别只在引擎跑在哪：本机跑烧的是手机的空间与电，遥控烧的是电脑那头的配置。

## 三步起步卡

| 步 | 动作 | 细节 |
|---|---|---|
| 1 下包 | 到 [Releases](https://github.com/ccch1mneyyy/dsh-Go/releases) 或官网下载页 go.dshtui.com 下 APK | 常见手机选 arm64 包（当前最新版 dsh-go-1.0.11-arm64.apk）；x86_64 设备与模拟器的 x64 包在发布说明末尾的「其他版本下载」里；仓库没有 32 位 ARM 构建；`update.json`、`SHA256SUMS` 是自动更新与校验用的，不用手动下，GitHub 自动生成的 Source code 是源码包、不是安装包 |
| 2 首启选路 | 首次启动选「在本机安装运行环境」或「连接远程主机」 | 只遥控就不必在手机上装本机运行环境；按系统提示允许该安装来源 |
| 3 配模型与凭据 | 为所选主机配置模型和所需凭据，再开始对话 | 部分远程渠道要在主机侧配置；模型请求发给你配的提供方，联网计费走你在提供方的账户 |

## 后台保活卡（换机型必读）

部分系统的省电策略会拦住后台进程，长任务跑着跑着就断。dsh-Go 发现后台被拦会提醒你，并直达对应的放行设置——vivo、小米、华为、荣耀、OPPO 都有专门入口。装完先做三件事：

1. **电池设置**：到 系统设置 → 电池（或应用耗电管理）→ dsh-Go，选「无限制 / 允许后台运行」，关掉自动冻结。
2. **自启动**：在手机管家/应用管理里把 dsh-Go 的自启动打开（小米、vivo、OPPO 尤其要单独开）。
3. **最近任务锁定**：把 dsh-Go 从最近任务里划掉前先锁定卡片，防止一键清理把长任务一起清掉。

逐品牌逐项清单见 [examples/机型后台保活设置速查.md](examples/机型后台保活设置速查.md)。

## 手机操控：三档确认怎么选

开启无障碍等权限后，本机引擎能读屏、点按、输入（只对正常模式下的本机引擎开放；不打扰模式另需 Android 14 及以上与 Shizuku 或自连 ADB）。确认分三档随你选：

| 档 | 行为 | 什么时候用 |
|---|---|---|
| 每次确认 | 每个动作先停下来等你点头 | 刚上手、或在不熟悉的 App 里操作时 |
| 按规则放行 | 你预先放行的应用与动作直接过，其余仍要确认 | 日常用熟了之后的主力档 |
| 免确认 / 解除限制 | 动作直接执行，保护最少 | 只在你清楚风险、且设备上没有支付与银行信息时短时用 |

硬线（原仓口径）：**支付、密码、验证码等敏感操作默认交还给你本人**，不进自动流程。放宽应用规则或解除限制之前，先想清楚这台手机里装了什么。

## 和 Mika 的区别（一句分清）

| | Mika（第 29 期） | dsh-Go（本期） |
|---|---|---|
| 定位 | 住在手机里、替你操作各类 App 的通用手机操作 agent | 把编程 harness 本体装进手机，或用手机遥控电脑上的编程 agent |
| 干的活 | 点外卖、回消息、刷应用这类日常操作 | 写代码、跑命令、盯长任务、批工具审批 |
| 引擎跑在哪 | 手机上，面向手机 App | 手机本机（内置 Linux 环境）或你电脑/服务器上的 dsh |

简单说：Mika 帮你用手机，dsh-Go 帮你带着编程 agent 走。

## 远程连接的边界（先知道再连）

DSHarness Remote（由李国宝开发）当前有几处限制（原仓自述）：只支持图片附件、不能在 App 内打开网页版、插件管理限于开关、不支持 DS Bot 与对话日志导出。功能随主机与连接方式不同，连之前先对一遍你的用法踩不踩这几条。

## 诚实标注区

- **社区非官方项目**：dsh-Go 与 DeepSeek 无隶属、不代表 DeepSeek（原仓自述）；它基于开源的 DeepSeek Harness 构建，手机上运行的是 DSH 引擎。
- **签名不同的早期测试包不能覆盖安装**：装过签名不同的早期测试包，须先卸载旧版才能装新版；卸载会清空对话、Linux 环境和设置，先导出要留的东西（原仓自述）。
- **本机跑不等于离线**：模型请求仍发给你配置的提供方，需要联网、按你在提供方的账户计费；开启手机操控后，任务需要的屏幕文字可能发给模型，支持看图的模型还可能收到截图（原仓自述）。
- **许可证分两层**：代码以 AGPL-3.0 发布，其中 `sdk/` 与 `examples/` 为 MIT；但 **dsh-Go 的名称与标识、吉祥物 Deepy 与鲸娘不在开源授权范围内**（见上游 ASSETS.md），以修改版身份再发布要换自己的名称与素材（原仓自述）。
- **工具会产生真实影响**：本机或远程主机上的命令、文件修改与手机操控可能造成数据丢失、账号或资金损失；确认机制不能消除所有风险，别让 AI 无人值守处理不可逆或高风险任务，重要结果自己核验（原仓风险提示）。
- **匿名统计默认开启**：可在首次引导或「设置 → 隐私与分享」关闭（原仓自述）。
- **本周势头**：11,277 ★ / 513 forks（2026-11-05 原仓页实测，证据 A）；Trendshift 全语言日榜第 1（2026-10-30，原仓自挂徽章，证据 B）。

---

## English (summary)

dsh-Go (11,277 stars / 513 forks as of 2026-11-05, AGPL-3.0) is a community Android client for DeepSeek Harness (dsh). It runs dsh right on your phone — the app installs an Ubuntu + Node.js runtime in-app, no root and no Termux — or it drives the dsh on your computer over SSH or DSH Remote, continuing the same conversation. Pick your route first: **on-device** needs about 1 GB free for the runtime and suits people away from a computer; **remote-only** installs nothing on the phone and is the safer first step for beginners and low-memory phones.

Getting started takes three steps: (1) download the APK from GitHub Releases or go.dshtui.com — most phones want the arm64 package (currently dsh-go-1.0.11-arm64.apk); the x64 build for x86_64 devices and emulators sits under "Other builds" at the end of the release notes, and there is no 32-bit ARM build; (2) on first launch, choose the on-device runtime or a remote host; (3) configure a model and its credentials for that host, then start chatting. It needs Android 8.0 (API 26) or later and is distributed as a sideloaded APK, not via Google Play.

Two cards save most of the pain. **Background survival**: aggressive battery savers on vivo, Xiaomi, Huawei, Honor and OPPO kill long tasks; the app detects this and deep-links to the right allowlist setting — set battery to unrestricted, enable autostart, and lock the task card. **Phone control**: after you grant permissions such as Accessibility, the local engine can read the screen and tap for you, with three confirmation levels (confirm every action / allow by rules you set / no-confirmation with limits lifted); sensitive screens — payments, passwords, verification codes — are handed back to you by default.

Honest notes: this is an unofficial community project, not affiliated with DeepSeek; an early test build signed with a different key cannot be updated in place — uninstalling first wipes chats, the Linux environment and settings; running locally is not offline — model requests still go to the provider you configure and bill your account there; the code is AGPL-3.0 (with `sdk/` and `examples/` under MIT), but the dsh-Go name and logo and the Deepy and Whale girl mascots are **not** covered by the open-source license. Not to be confused with Mika, a general phone-operating agent: dsh-Go puts a coding harness itself on your phone, or lets your phone remote-control the coding agent on your computer — the work is code.

---

## Español (guía rápida — traducción de estudio, pendiente de revisión por un hablante nativo)

dsh-Go (11.277 estrellas / 513 forks a 5 de noviembre de 2026, AGPL-3.0) es un cliente Android comunitario de DeepSeek Harness (dsh). Ejecuta dsh directamente en tu teléfono — la app instala un entorno Ubuntu + Node.js dentro de la propia app, sin root y sin Termux — o controla por SSH o DSH Remote el dsh de tu computadora, continuando la misma conversación. Elige primero tu ruta: **en el teléfono** necesitas unos 1 GB libres para el entorno y sirve si estás lejos de la computadora; **solo remoto** no instala nada en el teléfono y es el primer paso más seguro para principiantes y teléfonos con poca memoria.

Empezar lleva tres pasos: (1) descarga el APK desde GitHub Releases o desde go.dshtui.com — la mayoría de los teléfonos usa el paquete arm64 (hoy, dsh-go-1.0.11-arm64.apk); el paquete x64 para dispositivos x86_64 y emuladores está en «Other builds», al final de las notas de la versión, y no hay compilación ARM de 32 bits; (2) al primer inicio, elige el entorno local o un host remoto; (3) configura un modelo y sus credenciales para ese host y empieza a conversar. Requiere Android 8.0 (API 26) o superior y se distribuye como APK de instalación manual, no por Google Play.

Dos tarjetas te ahorran casi todos los problemas. **Supervivencia en segundo plano**: el ahorro de batería agresivo de vivo, Xiaomi, Huawei, Honor y OPPO mata las tareas largas; la app lo detecta y te lleva directo al ajuste de permiso correspondiente — pon la batería en «sin restricciones», activa el inicio automático y bloquea la tarjeta en tareas recientes. **Control del teléfono**: tras conceder permisos como Accesibilidad, el motor local puede leer la pantalla y tocar por ti, con tres niveles de confirmación (confirmar cada acción / permitir según reglas que tú defines / sin confirmación con límites levantados); las pantallas sensibles — pagos, contraseñas, códigos de verificación — vuelven a ti por defecto.

**Notas honestas**: es un proyecto comunitario no oficial, sin afiliación con DeepSeek; una versión de prueba temprana firmada con otra clave no se puede actualizar encima — desinstalar primero borra las conversaciones, el entorno Linux y los ajustes; funcionar en local no es funcionar sin conexión: las peticiones al modelo siguen yendo al proveedor que configures y se cobran en tu cuenta allí; el código es AGPL-3.0 (con `sdk/` y `examples/` en MIT), pero el nombre y el logotipo de dsh-Go y las mascotas Deepy y Whale girl **no** están cubiertos por la licencia de código abierto. No confundir con Mika, un agente general que opera apps del teléfono: dsh-Go mete el propio harness de programación en tu teléfono, o deja que tu teléfono controle a distancia el agente de programación de tu computadora — el trabajo es código.

---

## Português (guia rápido — tradução de estudo, aguardando revisão de um falante nativo)

O dsh-Go (11.277 estrelas / 513 forks em 5 de novembro de 2026, AGPL-3.0) é um cliente Android comunitário do DeepSeek Harness (dsh). Ele roda o dsh direto no seu telefone — o app instala um ambiente Ubuntu + Node.js dentro do próprio app, sem root e sem Termux — ou comanda por SSH ou DSH Remote o dsh do seu computador, continuando a mesma conversa. Escolha primeiro a sua rota: **no telefone** você precisa de cerca de 1 GB livres para o ambiente e serve para quem está longe do computador; **só remoto** não instala nada no telefone e é o primeiro passo mais seguro para iniciantes e telefones com pouca memória.

Começar leva três passos: (1) baixe o APK no GitHub Releases ou em go.dshtui.com — a maioria dos telefones usa o pacote arm64 (hoje, dsh-go-1.0.11-arm64.apk); o pacote x64 para aparelhos x86_64 e emuladores fica em «Other builds», no fim das notas da versão, e não há build ARM de 32 bits; (2) na primeira abertura, escolha o ambiente local ou um host remoto; (3) configure um modelo e suas credenciais para esse host e comece a conversar. Exige Android 8.0 (API 26) ou superior e é distribuído como APK de instalação manual, não pela Google Play.

Dois cartões evitam quase toda a dor de cabeça. **Sobrevivência em segundo plano**: a economia de bateria agressiva de vivo, Xiaomi, Huawei, Honor e OPPO mata tarefas longas; o app detecta isso e leva você direto à configuração de permissão certa — deixe a bateria «sem restrições», ative a inicialização automática e trave o cartão em tarefas recentes. **Controle do telefone**: depois de conceder permissões como Acessibilidade, o motor local pode ler a tela e tocar por você, com três níveis de confirmação (confirmar cada ação / permitir por regras que você define / sem confirmação com limites levantados); as telas sensíveis — pagamentos, senhas, códigos de verificação — voltam para você por padrão.

**Notas honestas**: é um projeto comunitário não oficial, sem afiliação com a DeepSeek; uma versão de teste antiga assinada com outra chave não pode ser atualizada por cima — desinstalar antes apaga as conversas, o ambiente Linux e as configurações; rodar localmente não é rodar offline: as requisições ao modelo continuam indo ao provedor que você configurar e são cobradas na sua conta lá; o código é AGPL-3.0 (com `sdk/` e `examples/` em MIT), mas o nome e o logotipo do dsh-Go e os mascotes Deepy e Whale girl **não** são cobertos pela licença de código aberto. Não confundir com o Mika, um agente geral que opera apps do telefone: o dsh-Go coloca o próprio harness de programação no seu telefone, ou deixa seu telefone controlar remotamente o agente de programação do seu computador — o trabalho é código.

---

## 来源与声明

- 灵感来源 / Source / Fuente / Fonte: [ccch1mneyyy/dsh-Go](https://github.com/ccch1mneyyy/dsh-Go)（上游代码 AGPL-3.0；`sdk/`、`examples/` 为 MIT；名称、标识与吉祥物素材不在开源授权内，见上游 ASSETS.md）
- 本仓是个人学习整理：内容用我自己的话总结自上游公开文档，不搬运原文；安装步骤、保活品牌清单与远程连接限制以 2026-11-05 的上游 README（简中与英文）及 Releases 页为准，上游迭代后请以官方文档为最终依据。
- 西语、葡语部分为学习译稿，待母语校对。Las secciones en español y portugués son traducciones de estudio pendientes de revisión nativa.
- License: MIT © 2026 Guangyi Zhao（本仓自有内容；上游项目的 AGPL-3.0 与素材限制见上）
