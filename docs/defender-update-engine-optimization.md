# Microsoft Defender – Otimização de Atualização de Engines (Beta Channel)

## Contexto

Durante análise dos indicadores no Microsoft Defender for Endpoint, foi identificado que três componentes essenciais estavam desatualizados:

- **Antivirus Security Intelligence**
- **Antivirus Platform Version**
- **Antivirus Engine Version**

Essa defasagem impactava o tempo de resposta em incidentes e análise de IOC.

---

## Root Cause

A documentação da Microsoft confirma que, quando o canal de atualização está configurado para:

- **Canal amplo (Broad)**

As atualizações são aplicadas apenas após o ciclo completo, atrasando a propagação.

Nos dispositivos gerenciados pela organização, esse era o comportamento vigente.

---

## Solução Aplicada

Foi configurado o **Beta Channel** para:

- Atualizações de mecanismo
- Atualizações de plataforma
- Atualizações de inteligência

Isso permite recebimento imediato de novas versões, reduzindo latência.

### Configuração no Intune
(prints serão inseridos depois)

---

## Resultado Observado

Após a alteração:

- Engines foram atualizadas muito mais rapidamente
- Indicadores no Defender ficaram em conformidade
- Redução do backlog de versões defasadas

### Antes do ajuste:
![Antes do ajuste](/docs/images/engine-metrics-before.png)



### Após o ajuste:
(imagem será inserida aqui)

---

## Observações Técnicas

- Canal Beta é seguro e documentado pela Microsoft
- Benéfico para ambientes com SOC ativo
- Mitigação rápida em emergências

---

## 📚 Referências

- Documentação Oficial Microsoft
- Defender for Endpoint – Update Mechanisms

