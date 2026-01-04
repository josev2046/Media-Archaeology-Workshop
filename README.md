[![DOI](https://zenodo.org/badge/1126896397.svg)](https://doi.org/10.5281/zenodo.18134825)

# Addendum: Media archaeology workshop
## Anexo: Taller de arqueología de medios

This workshop is integrated into the course **"Casos de estudio para la investigación en humanidades digitales (curso 2025-26)"** at **Universidad Pablo de Olavide, Sevilla**. It serves as a practical extension of the module on **obsolescence and media fragmentation**, providing students with hands-on experience in the physical and digital recovery of 8-bit computing heritage.

Este taller se integra en la asignatura **"Casos de estudio para la investigación en humanidades digitales (curso 2025-26)"** de la **Universidad Pablo de Olavide, Sevilla**. Sirve como una extensión práctica del módulo sobre **obsolescencia y fragmentación de medios**, proporcionando al alumnado experiencia directa en la recuperación física y digital del patrimonio informático de 8 bits.

---

### English version: From bit to memory
**Title: Practical case study on software preservation and hardware obsolescence**

#### Context and rationale
Within the framework of "obsolescence and media fragmentation," this practical workshop moves from theory to physical interaction with legacy hardware. The Sinclair ZX Spectrum (1982) serves as a primary case study for understanding the fragility of magnetic storage and the complexities of preserving software as cultural heritage. Students will engage with the challenges of recovering data from a format that is physically degrading and technically orphaned.

#### Specific content
* **Magnetic media forensics:** analysing the physical degradation of cassette tapes. Techniques for audio sampling to facilitate data recovery by converting analogue signals into digital bitstreams.
* **Migration vs. emulation:** the use of modern interfaces such as SD and flash storage on original hardware. This includes a debate on authenticity: whether the tactile and sensory experience of the user is a vital part of the historical record.
* **Documenting orphaned digital objects:** addressing the challenges in the categorisation of software lacking machine-readable metadata. We will apply minimum standards for the description of obsolete technological artefacts.

#### Learning objectives
* Identify the inherent risks of data loss in consumer-grade magnetic storage formats.
* Execute a basic preservation workflow, ranging from physical hardware maintenance to the creation of digital tape images in .tzx or .tap formats.
* Contextualise 1980s software as a form of social memory requiring specific archival strategies beyond simple digitisation.

---

### Versión española: Del bit a la memoria
**Título: Estudio de caso práctico sobre preservación de software y obsolescencia de hardware**

#### Justificación
En el marco del estudio de la "obsolescencia y fragmentación de medios", este taller práctico traslada la teoría a la interacción física con el hardware original. El Sinclair ZX Spectrum sirve como estudio de caso principal para entender la fragilidad del soporte magnético y la complejidad de la preservación del software como patrimonio cultural. Los estudiantes se enfrentarán a los desafíos de recuperar datos de un formato en degradación física y técnicamente huérfano.

#### Contenidos específicos
* **Forense de medios magnéticos:** análisis de la degradación física de las cintas de casete. Técnicas de muestreo de audio para la recuperación de datos mediante la conversión de señales analógicas a flujos de datos digitales.
* **Migración vs. emulación:** uso de interfaces modernas (SD/flash) en hardware original. Debate sobre la autenticidad: si la experiencia táctil y sensorial del usuario es una parte vital del registro histórico.
* **Documentación de objetos digitales huérfanos:** desafíos en la catalogación de software que carece de metadatos legibles por máquina. Aplicación de estándares mínimos para la descripción de artefactos tecnológicos obsoletos.

#### Objetivos de aprendizaje
* Identificar los riesgos inherentes de pérdida de datos en los formatos de almacenamiento magnético doméstico.
* Ejecutar un flujo de trabajo de preservación básico: desde el mantenimiento del hardware físico hasta la creación de imágenes de cinta digitales (.tzx/.tap).
* Contextualizar el software de los años 80 como una forma de memoria social que requiere estrategias de archivo específicas más allá de la simple digitalización.

---

## Project Z80-Forensics: ZX Spectrum Digital Preservation

A technical framework for the **magnetic media forensics**, **migration**, and **archival documentation** of Sinclair Spectrum software. This repository provides the standards for converting physical analogue degradation into permanent digital records.

## 1. Magnetic Media Forensics
The primary goal is the recovery of bitstreams from degraded ferric oxide tapes. 

### Pulse Detection Logic
Data recovery is based on the timing of Z80 $T-states$ (clock cycles). The hardware interprets the signal based on the duration between zero-crossings. On a standard 3.5MHz machine, we look for:

* **Pilot Pulse:** 2,168 $T-states$ (approx. 619 $\mu s$)
* **'0' Bit (Short):** 855 $T-states$ per pulse (approx. 244 $\mu s$)
* **'1' Bit (Long):** 1,710 $T-states$ per pulse (approx. 489 $\mu s$)



### Forensic Workflow
1.  **Azimuth Correction:** Physical alignment of the playback head to maximise high-frequency response.
2.  **Bilateral Sampling:** Capturing audio at 24-bit/96kHz to ensure the Nyquist frequency comfortably exceeds the signal harmonics.
3.  **Normalisation:** Removing DC offset and correcting phase inversion to ensure clean zero-crossing detection.

---

## 2. Migration vs. Emulation
This project distinguishes between the "logic" of the software and the "experience" of the hardware.

### Hardware Migration
We support the use of modern interfaces on original 48K/128K hardware to bypass the inherent instability of magnetic media:
* **DivMMC / SD Storage:** Bypassing tape instability while retaining original Z80 CPU cycles and ULA timing.
* **Flash ROM Cartridges:** Providing instantaneous software access through the rear expansion port.

### The Authenticity Debate
We document the **Sensory Contextual Record**. A preservation entry is not complete without noting the tactile and environmental factors that define the historical record:
* **Keyboard Type:** Rubber mat ("dead flesh") vs. Sinclair plastic keys.
* **Loading Duration:** The temporal experience of the loading process as a component of the user's focus.
* **Visual Artefacts:** NTSC/PAL composite "colour bleed" and the distinctive attribute clash.

---

## 3. Documenting Orphaned Objects
To address software lacking machine-readable metadata, we adhere to a **Minimum Archival Standard** for obsolete technological artefacts.

### Metadata Schema
Every recovered `.TZX` or `.TAP` file must be accompanied by a `metadata.json` containing:

| Key | Description | Requirement |
| :--- | :--- | :--- |
| `uuid` | Unique SHA-1 hash of the bitstream | Mandatory |
| `machine_type` | Target hardware (16K, 48K, 128K, +2, +3) | Mandatory |
| `media_origin` | Physical tape brand and batch (e.g., C60 Ferric) | Recommended |
| `protection_id` | Identification of custom loaders (e.g., Speedlock) | Optional |

---

## 4. Condition Assessment Rubric
Before attempting digital recovery, the physical carrier must be graded to prevent hardware damage (e.g., oxide shedding fouling the playback head).



| Grade | Classification | Characteristics | Action Required |
| :--- | :--- | :--- | :--- |
| **A** | Pristine | No visible wear; felt pad intact; tape moves freely. | Direct sampling. |
| **B** | Worn | Minor shell scuffing; slight "railroading" on tape edges. | Clean heads after every pass. |
| **C** | Degraded | Sticky-shed evidence; visible "cinching" (folds) in tape. | Requires dehydration/baking. |
| **D** | Critical | Active mould (white spots); snapped leader; missing pad. | Specialist isolation/repair only. |

---

