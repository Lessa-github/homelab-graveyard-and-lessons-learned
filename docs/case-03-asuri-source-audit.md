# Case 03: Static Security Code Audit & Disqualification of Asuri/Azuri

During pre-deployment Static Application Security Testing (SAST) of the open-source Asuri repository, our AppSec audit identified multiple disqualifying liabilities:
1. **Unpinned Vulnerable Dependencies:** Outdated npm packages containing critical CVEs allowing Remote Code Execution (RCE).
2. **Command Injection Risks:** Insufficient parameter sanitization prior to system-level subshell invocation.
3. **Overprivileged Runtime Requirements:** Unnecessary root permission demands incompatible with unprivileged LXC security baselines.

**Engineering Verdict:** The tool was summarily disqualified and blacklisted from homelab production deployment.
