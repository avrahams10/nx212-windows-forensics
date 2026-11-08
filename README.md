# NX212 — Windows Forensics Automation

**Bash-Orchestrated Digital Forensic Examination | Authorized Laboratory Evidence**  
**Cybersecurity portfolio case study | Avraham Thomas**

## Overview

NX212 began as my **original student-developed Bash workflow** for coordinating several forensic tools through a guided interface. The original project brought disk/memory-image processing, candidate file carving, feature extraction, memory analysis, reporting, and ZIP packaging into one repeatable process.

Later **owner-directed, Codex-assisted** improvements introduced input checks, stage supervision, source-hash comparisons, bounded carving, Windows memory-profile handling, and clearer structured reporting. These are separate development stages; later functionality is not presented as entirely unaided original student code or as production-validated forensic software.

## Workflow and tool roles

*Conceptual tool-role diagram; not a captured execution trace.*

```text
            Authorized forensic image
                       |
               Guided Bash workflow
                       |
       +---------------+---------------+
       |               |               |
     Foremost     Bulk Extractor     Binwalk
       |               |               |
   File candidates   Features/PCAP   Signatures
                       |
                Volatility 2
          Process, hive and socket views
                       |
             Analyst interpretation
                       |
             Reports and archive
```

The workflow also uses `strings` for readable artifacts and supports separate packet review using Wireshark/TShark when appropriate. Tool output needs analyst validation; a hit is not automatically an incident finding.

## Recorded laboratory evidence

An October 2026 project record describes the later workflow operating on an authorized **512 MiB Windows XP SP3 x86 memory image**. The figures below are **reported in the approved case study** and were not re-created by running the tools for this GitHub edition.

| Stage | Recorded outcome | Interpretation limit |
| --- | --- | --- |
| **Foremost** | **181** file-carving candidates | Not authenticated files or malware confirmations |
| **Bulk Extractor** | **2,552** feature records across six categories | Occurrences can repeat and are not 2,552 incidents |
| **Reconstructed PCAP** | **133** packet records | Epoch-zero timestamps do not establish a reliable event timeline |
| **Binwalk** | **6** signature detections and one bounded **1 MiB** raw carve | Signature matches do not guarantee complete extracted files |
| **Volatility 2** | `pslist` **17**, `hivelist` **13**, `sockets` **15**, `sockscan` **15** output rows | Memory structures are investigative leads, not confirmed compromise |
| **Reporting / integrity** | Matching source SHA-256 checkpoints and ZIP validation **reported** | Not continuous write protection or independent inspection of final archive bytes |

### Cross-tool investigation example

A reconstructed packet capture contained an **HTTP POST** from one lab host toward a remote endpoint on port 8080. In a separate analyst follow-up, memory review found a process-associated connection to the same remote endpoint. This is useful for further investigation, but the POST source port was **not confirmed**. Therefore the evidence does **not** establish that a particular process issued that HTTP request. Neither observation proves malware, command-and-control, or data exfiltration.

The packet records' timestamps cannot support a trustworthy chronological reconstruction. A separate training image also produced ambiguous Windows memory-profile candidates, so broader compatibility was **not established**.

## Evidence provenance and interpretation

- **June 2025 student demonstration:** historical screenshots of workflow orchestration, reporting, and ZIP output. These are not the October 2026 exercise.
- **Safety-adjusted original-workflow test:** supports a limited workflow comparison, not an unchanged-original run or performance benchmark.
- **October 2026 improved-workflow record:** supports the reported outcomes above. The final source/export bytes and underlying raw execution records were not independently inspected for this README.

The original workflow is my student work. Later improvements and documentation included **owner-directed Codex assistance**.

## Practical lessons and limitations

Forensic candidate counts, inferred indicators, source hashes, and archive integrity checks answer **different questions**. Hash equality at recorded checkpoints is not a continuous write-blocking guarantee; timeouts and storage monitoring do not create a hard forensic sandbox. The project does **not** claim a verified malicious incident, formal chain of custody, universally compatible analysis, or production-readiness.

## Repository contents

This repository contains a **documentation-only case study**. No forensic images, recovered files, PCAPs, feature lists, identifiable endpoints, executables, original school exhibits, scripts, or private case-study masters are included. Each prospective code or evidence addition requires independent authorization, provenance, and privacy review.
