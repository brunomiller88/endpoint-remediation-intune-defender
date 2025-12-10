Remediação Residual WinRAR – CVE-2025-6218

Quando a vulnerabilidade CVE-2025-6218 (relacionada ao WinRAR) aparece no Microsoft Defender, mesmo após:

remover o WinRAR via Defender
ou criar um script de remoção via Intune

Ainda pode continuar aparecendo como vulnerável no inventário.

Motivo

O software WinRAR deixa uma chave residual no registro:
HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\WinRAR archiver

O Defender entende que essa chave significa que o software ainda está instalado, mesmo que o executável já tenha sido removido.

Solução aplicada

Identifiquei essa chave no inventário do dispositivo pelo Defender e então criei uma remediação via Intune com:

✔ Um script de detecção

✔ Um script de remoção

✔ Saída visível (exit code) para acompanhamento no Intune

SCRIPT DE DETECÇÃO (Detection Script)

<#
Detecção – Verifica se ainda existe a chave de desinstalação do WinRAR

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\WinRAR archiver

Exit 0 = chave NÃO existe (compliance OK)
Exit 1 = chave existe (problema detectado – será contada no Intune)
#>

$regPath = 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\WinRAR archiver'

if (Test-Path -Path $regPath) {
    Write-Output "DETEÇÃO: Chave do WinRAR ENCONTRADA em $regPath"
    exit 1
}
else {
    Write-Output "DETEÇÃO: Chave do WinRAR NÃO encontrada em $regPath"
    exit 0
}

SCRIPT DE CORREÇÃO (Remediation Script)

<#
Remediação – Remove a chave de desinstalação do WinRAR

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\WinRAR archiver

Exit 0 = executado com sucesso (chave removida ou já não existia)
Exit 1 = erro ao tentar remover
#>

$ErrorActionPreference = 'Stop'
$regPath = 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\WinRAR archiver'

try {
    if (Test-Path -Path $regPath) {
        Remove-Item -Path $regPath -Recurse -Force
        Write-Output "REMEDIAÇÃO: Chave do WinRAR REMOVIDA de $regPath"
    }
    else {
        Write-Output "REMEDIAÇÃO: Chave do WinRAR já NÃO existia em $regPath"
    }

    exit 0
}
catch {
    Write-Error "REMEDIAÇÃO: ERRO ao remover a chave $regPath. Detalhes: $($_.Exception.Message)"
    exit 1
}

Resultado no Intune

Após implementar:

Máquinas detectadas aparecem como exit 1

Máquinas corrigidas aparecem como exit 0


Isso te dá visibilidade clara no portal de remediações.

Benefícios para o ambiente corporativo

Elimina falsos positivos no Defender

Corrige score de vulnerabilidade

Remove resíduos de software

Aumenta governança de endpoint

Automatiza compliance

Autor

Bruno Jung Miller
Analista de Cibersegurança | Endpoint Protection | Intune | Defender | Entra ID | Exchange | Pureview | Admin Center
