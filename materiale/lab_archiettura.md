# Laboratorio — Cosa c'è dentro al nostro personal computer? 

## 1. Via grafica

**Windows**: 

Premi `Ctrl + Maiusc + Esc` → *Gestione attività* → scheda **Prestazioni**. 

Lì trovi CPU (nome, core, processori logici, velocità base), Memoria (totale, velocità, slot usati) e Disco (indica se è SSD o HDD). 

In alternativa: *Impostazioni → Sistema → Informazioni su*.

**macOS**: 

menu (mela)  → **Informazioni su questo Mac** (chip e memoria). 

Per il tipo di archiviazione: “Ulteriori info…”.

**Linux**: 

*Impostazioni → Sistema → Informazioni sul sistema* (varia col desktop). 

Qui però il terminale è nettamente più informativo: vedi sotto.

---

## 2. Via terminale

Apri il terminale:
- **Windows**: cerca *PowerShell* nel menu Start.
- **macOS**: *Applicazioni → Utility → Terminale*.
- **Linux**: `Ctrl + Alt + T` (o cerca *Terminal*).

Poi lancia il comando corrispondente a ciò che vuoi sapere, tra quelli indicati sotto: 

### Modello CPU, core fisici e logici, frequenza

| | Comando |
|---|---|
| **Windows** | `Get-CimInstance Win32_Processor \| Select Name,NumberOfCores,NumberOfLogicalProcessors,MaxClockSpeed` |
| **macOS** (Intel) | `sysctl -n machdep.cpu.brand_string` &nbsp;+&nbsp; `sysctl hw.physicalcpu hw.logicalcpu` |
| **macOS** (Apple Silicon, M1/M2/M3…) | `system_profiler SPHardwareDataType` |
| **Linux** | `lscpu` |

### RAM: totale, tipo (DDR4 / DDR5), velocità

| | Comando |
|---|---|
| **Windows** | `Get-CimInstance Win32_PhysicalMemory \| Select Capacity,Speed,Manufacturer,FormFactor` |
| **macOS** | `sysctl hw.memsize` &nbsp;(totale) &nbsp;·&nbsp; tipo/velocità: `system_profiler SPMemoryDataType` |
| **Linux** | `free -h` &nbsp;(totale) &nbsp;·&nbsp; tipo/velocità: `sudo dmidecode --type memory` |

### Disco: è un SSD o un HDD? quanto è capiente?

| | Comando |
|---|---|
| **Windows** | `Get-PhysicalDisk \| Select FriendlyName,MediaType,Size` |
| **macOS** | `diskutil info / \| grep -i solid` &nbsp;→ *Solid State: Yes/No* |
| **Linux** | `lsblk -d -o NAME,ROTA,SIZE,MODEL` &nbsp;→ colonna `ROTA`: **1 = HDD**, **0 = SSD** |

### Tutto in un colpo solo (panoramica)

| | Comando |
|---|---|
| **Windows** | `systeminfo` |
| **macOS** | `system_profiler SPHardwareDataType SPMemoryDataType SPStorageDataType` |
| **Linux** | `sudo lshw -short` |

> **Note pratiche**
> - Su Windows `Capacity` è in **byte**: dividi per `1073741824` per avere i **GB** (es. 8589934592 → 8 GB).
> - Su Linux i comandi con `sudo` chiedono la password e mostrano più dettagli; senza `sudo`, `free -h` ti dà comunque il totale della RAM.
> - Su **Mac Apple Silicon** il comando sulla RAM non mostra “slot / tipo / velocità”: è normale, la memoria è *unificata* e saldata dentro il chip (ne parliamo qui sotto).

---

