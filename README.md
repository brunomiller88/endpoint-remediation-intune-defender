# 🔐 Endpoint Remediation & Governance – Intune & Defender

Este repositório contém scripts, remediações e documentação técnica aplicadas a ambientes corporativos que utilizam:

- Microsoft Defender for Endpoint
- Microsoft Intune (Endpoint Manager)
- Inventário e governança de vulnerabilidades
- Remoção e auditoria de software
- Correções relacionadas a CVEs
- Automação de compliance

---

## 📌 Objetivo do Repositório

Criar uma coleção prática e validada de:
- Scripts PowerShell para remediação e detecção no Intune
- Mitigações e ajustes para vulnerabilidades detectadas no Defender
- Análise técnica e documentação para histórico e portfólio

---

## 📂 Conteúdo

| Área | Descrição |
|-----|-----------|
| `Remediações` | Scripts de correção para softwares e chaves residuais |
| `Detecções`   | Scripts que auditam estado do sistema via Intune |
| `Documentação` | Explicações técnicas e análise de CVEs |
| `Governança` | Ajustes e mitigação preventiva em endpoints |

---

## 🛠️ Casos Documentados (CVE e correções)

### ✔️ CVE-2025-6218 – WinRAR (Chave Residual no Registro)
Documentação completa ➜ [`winrar-registry-fix.md`](./winrar-registry-fix.md)

**Resumo do caso:**
- Mesmo após o Defender remover o WinRAR
- A vulnerabilidade continuava aparecendo no inventário
- A causa era chave residual em:  
  `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\WinRAR archiver`
- Scripts foram criados para detecção + remoção

---

## 🧰 Tecnologias utilizadas

- PowerShell  
- Intune Remediation  
- Microsoft Defender for Endpoint  
- Auditoria por CVE  
- Governança de vulnerabilidade  

---

## 📈 Resultado esperado

- Remediações visíveis em relatórios
- Melhoria real do Secure Score
- Redução de falsos positivos
- Documentação corporativa reutilizável

---

Autor

**Bruno Jung Miller**  
Analista de Cibersegurança  
Especialista em Intune, Defender,Entra ID, Pureview, Exchange, Admin Center - Governança e Automação de Remediações.

---

## 📌 Atualizações

Este repositório será continuamente atualizado com:
- Novas remediações
- Documentação de CVEs
- Análises técnicas realistas
