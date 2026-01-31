# MikroTik Architect v7.7 🏗️

**A ferramenta definitiva para dimensionamento de hardware e automação de scripts RouterOS.**

---

## 🎯 Visão Geral

O **MikroTik Architect** é uma solução *client-side* (Single Page Application) projetada para eliminar o *achismo* no planejamento de redes MikroTik. A proposta é simples e direta: **decisão técnica baseada em dados**, não em feeling.

A ferramenta entrega:

- Dimensionamento de hardware (*Sizing*) orientado por heurísticas reais  
- Automação da geração de scripts RouterOS  
- Forte integração com ecossistemas de Hotspot, com destaque para o **WiFeed**

Esqueça planilhas manuais. O sistema calcula a carga projetada de **CPU** e **RAM** considerando tráfego, firewall e serviços ativos, e retorna um **veredito técnico imediato** sobre a viabilidade do equipamento escolhido.

---

## 🚀 Funcionalidades Chave

### 1. Dimensionamento de Hardware Inteligente

- **Cálculo Heurístico**  
  Estimativa de consumo de CPU e RAM baseada em:
  - Usuários simultâneos  
  - Largura de banda  
  - Tipo de WAN (PPPoE / DHCP)  
  - Serviços ativos  

- **Database de Hardware**  
  Base técnica com modelos populares:
  - RB750Gr3  
  - RB4011  
  - CCR1036  
  - Outros  
  Inclui pontuação de CPU normalizada para comparação objetiva.

- **Sugestão de Upgrade (Upsell Inteligente)**  
  Caso o hardware esteja saturado, o sistema recomenda automaticamente o próximo modelo capaz de suportar:
  - A carga projetada  
  - +20% de *headroom* operacional  

- **Dashboard em Tempo Real**  
  Visualização gráfica animada mostrando o impacto imediato de cada alteração de configuração.

---

### 2. Automação de Scripts (RouterOS)

- **Geração Full-Stack**  
  Criação de scripts `.rsc` completos, incluindo:
  - Identity  
  - Usuários  
  - Interfaces  
  - DHCP Server  
  - Pools  
  - NAT  
  - Rotas  

- **Perfis de Cenário (Templates)**  
  Predefinições inteligentes para cenários comuns:

  - 🏢 **Hotspot (WiFeed)**  
    Otimizado para alta densidade de usuários e filas dinâmicas  

  - 💼 **Corporativo**  
    Ênfase em Firewall, bloqueios (L7 / Content) e QoS  

  - 🏠 **Doméstico**  
    Configuração básica, enxuta e eficiente  

---

### 3. Integração Avançada WiFeed 📡

- **Parser de Script (`.rsc`)**  
  Leitura, interpretação e modificação de scripts de autoconfiguração do WiFeed  
  - Exemplo: `autoconfig-wif...rsc`

- **Editor Retrátil Dedicado**  
  Ajuste de parâmetros internos sem tocar diretamente no código:

  - **Walled Garden**  
    Detecção via *Regex* de todas as regras  
    - Ativação/desativação individual de domínios  

  - **Firewall Checker**  
    Listagem completa das regras importadas  
    - Toggle de regras de Firewall e NAT  

  - **Fix de Autenticação**  
    Detecção automática e injeção do parâmetro:  
    ```routeros
    require-message-auth=no
    ```  
    Compatível com versões legadas e novas do RouterOS.

  - **Ajuste Fino**  
    - Lease Time  
    - Pool de IPs  
    - Interface do Hotspot  

---

### 4. Calculadoras Utilitárias

- **Cálculo de Subnet (Bitwise)**  
  Calculadora precisa de Pool DHCP baseada em CIDR:
  - `/18` até `/30`

- **Conversor de Lease Time**  
  Suporte a múltiplos formatos:
  - `10m`  
  - `1h`  
  - `1d`  

---

## 🛠️ Stack Tecnológica

O projeto segue uma filosofia **no-build**, priorizando portabilidade e simplicidade operacional.

- **Core**  
  - HTML5 semântico  
  - CSS3 (Variáveis, Flexbox e Grid)  

- **Logic**  
  - Vanilla JavaScript (ES6+)  

- **Architecture**  
  - *Module Pattern* (`window.App`)  
  - Encapsulamento claro de estado e lógica  

- **UI/UX**  
  - Design System **Cyberpunkish Dark**  
  - Responsivo  
  - Uso de *Design Tokens* para consistência visual  

---

## 📦 Como Usar

1. **Não requer instalação**  
   - Sem Node.js  
   - Sem dependências  
   - Sem backend  

2. **Download**  
   - `MikroTik_Architect_v7_Complete.html`

3. **Execução**  
   - Abra em qualquer navegador moderno:
     - Chrome  
     - Edge  
     - Firefox  

4. **Configuração Básica**  
   - Selecione o modelo da RB  
   - Defina número de usuários  
   - Configure o link  

5. **Ajustes Avançados (Opcional)**  
   - Clique em **Avançado** para:
     - Pools manuais  
     - Usuários extras  
     - Regras de NAT  

6. **Integração WiFeed (Opcional)**  
   - Selecione o cenário **Hotspot**  
   - Faça upload do arquivo `.rsc` do WiFeed  
   - Ajuste as regras no painel dedicado  

7. **Geração Final**  
   - Clique em **Gerar Script Final**  
   - Copie ou baixe o arquivo `.rsc`  

---

## ⚠️ Disclaimer e Boas Práticas

> **“Trust, but verify.”**

Apesar do algoritmo de dimensionamento ser robusto, ele se baseia em **benchmarks sintéticos** e **cenários médios**. O desempenho real pode variar conforme:

- MTU / MSS  
- Quantidade de *filter rules*  
- Queues complexas  
- Scripts de terceiros  

### Recomendação Crítica

- Sempre valide o script em **ambiente de laboratório (lab)**  
- Nunca aplique diretamente em produção sem revisão  

O autor **não se responsabiliza** por indisponibilidades causadas por aplicação direta sem validação prévia.

---

## 🤝 Contribuição

Contribuições são incentivadas para evolução contínua da ferramenta.

Possíveis melhorias:
- Refinar pesos de cálculo de CPU (`cpu_pps_factor`)  
- Adicionar novos modelos ao `hardwareDB`  

### Workflow Recomendado

```bash
git checkout -b feature/NovoModeloRB
