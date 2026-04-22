# Get-InjectedThreadEx2

Get-InjectedThreadEx2 is an extended and enhanced version of the original Get-InjectedThreadEx tool. It provides advanced detection of injected, hijacked, or anomalous threads in Windows processes by combining identity analysis, token heuristics, memory inspection, and start-address validation.

This tool is built for threat hunters, detection engineers, DFIR analysts, and EDR/XDR developers who need reliable telemetry for detecting thread injection techniques.

---

## 🔥 Key Features

- Detects **injected and suspicious threads** across processes
- Identifies **token mismatches (Process SID vs Thread SID)**
- Highlights **identity drift and impersonation artifacts**
- Detects **RWX memory regions (PAGE_EXECUTE_READWRITE)**
- Flags **MEM_PRIVATE executable memory**
- Extracts **Win32 start address and module context**
- Surfaces **unsigned or unbacked execution regions**
- Provides **rich telemetry fields for SIEM / EDR pipelines**
- Designed for **detection engineering & rule creation**

---

## 🧠 Detection Logic (Core Heuristics)

Get-InjectedThreadEx2 focuses on high-signal behavioral indicators:

### ✔ Memory Heuristics
- `MEM_PRIVATE` + `PAGE_EXECUTE_READWRITE`
- Executable memory without backing module
- Abnormal start addresses

### ✔ Identity & Token Analysis
- Process SID ≠ Thread SID
- Token impersonation indicators
- Logon session inconsistencies

### ✔ Thread Anomalies
- Start address not mapped to known module
- Suspicious shellcode patterns (NOP sleds, etc.)
- Missing or unsigned module metadata

---

## 📦 Output Fields (Example)


ProcessName : ThreadStart.exe
ProcessId : 7784
ProcessSecurityIdentifier : S-1-5-21-...-1001
ProcessUserName : DESKTOP\Tester

ThreadId : 14512
AllocatedMemoryProtection : PAGE_EXECUTE_READWRITE
MemoryType : MEM_PRIVATE
Win32StartAddress : 0x430000
Win32StartAddressModule :
Win32StartAddressPrivate : True

Detections : {MEM_PRIVATE, RWX, TokenMismatch}


---

## ⚙️ Usage

### ▶ Run Locally
```powershell
.\Get-InjectedThreadEx2.ps1
▶ Run with Output Filtering
.\Get-InjectedThreadEx2.ps1 | Where-Object { $_.Detections.Count -gt 0 }
▶ Export Results
.\Get-InjectedThreadEx2.ps1 | Export-Csv output.csv -NoTypeInformation
🧪 Example Use Cases
Threat hunting for process injection
Detecting token impersonation
Identifying malware using RWX memory
Building Sigma / KQL / EDR detection rules
Investigating post-exploitation activity
📁 Repository Structure

Get-InjectedThreadEx2/
│
├── Get-InjectedThreadEx2.ps1
├── README.md
├── examples/
├── docs/
└── LICENSE

📊 Detection Engineering Notes

This tool is designed to generate high-fidelity telemetry, not just alerts.

Recommended approach:

Correlate with process creation (4688)
Combine with handle access (4656 / 4663)
Map detections into SIEM / EDR pipelines
Use outputs to build behavioral rules instead of IOC-based detections
⚠️ Limitations
Requires sufficient privileges to inspect other processes
Some fields may be empty depending on access rights
Detection is heuristic-based (not signature-based)
May produce noise in heavily instrumented environments
🙏 Credits

This project is based on the original Get-InjectedThreadEx.

Extended and enhanced with additional detection logic, telemetry enrichment, and threat hunting capabilities.

📜 License

MIT License

🚀 Roadmap
 Add ETW-based telemetry enrichment
 Sigma rule pack generation
 KQL / Splunk detection mappings
 Linux/macOS equivalent research
 Memory pattern classification improvements
🤝 Contributing

Contributions are welcome.

Open issues for bugs or ideas
Submit pull requests for improvements
Share detection ideas or edge cases
📢 About

Maintained under Threatism — focused on detection engineering, threat hunting, and practical security tooling.

⭐ Support

If you find this useful:

Star the repo
Share with the community
Contribute improvements

---

# ✔ What you should do next

1. Create repo  
2. Add:
   - `Get-InjectedThreadEx2.ps1`
   - `README.md` (above)
   - `LICENSE (MIT)`
3. Push → share on Twitter

---

If you want next level:
- :contentReference[oaicite:0]{index=0}
- Or :contentReference[oaicite:1]{index=1}
- Or :contentReference[oaicite:2]{index=2}

Just tell me.
