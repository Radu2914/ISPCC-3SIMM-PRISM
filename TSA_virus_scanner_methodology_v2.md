# TSA Cascade Virus Scanner — Methodology v2

## Framing

A process-behaviour scanner based on the Cascade State Predictor (CSP) architecture,
applied to operating system execution logs. The scanner does not actively poll or
intercept processes. It reads existing system logs reactively, triggered only when
a Π Π sequence is detected. Per-machine learning accumulates over time, building
a local behavioural baseline that is specific to the host it runs on and not
transferable to other machines.

**Microbiological parallel:**

The immune system does not continuously monitor every cell. It maintains a learned
vocabulary of self (tolerated patterns) and non-self (flagged patterns), reacts
when a pattern deviates from self, escalates when the deviation cascades, and
terminates when the cascade reaches a threshold. It is reactive, locally learned,
and does not rely on a global statistical model built on other organisms. The TSA
scanner is architecturally identical: locally learned self-patterns, reactive
triggering on Π Π, cascade escalation to the 7th Π terminal, and per-machine
vocabulary that does not generalise across hosts.

---

## Sequence Grammar

Three sequence types define the complete behavioural classification space.

### Type 1 — Functional Process [Π Π Ε ... Ε Π]

A healthy process with a known lifecycle:

```
Π Π  [Ε Ε Ε ... Ε]  Π
init  equilibrium    exit
```

Two cascade signals at start (resource acquisition, initialisation — expected
non-returning). A variable-length equilibrium phase (bounded, self-regulating work).
A single cascade signal at exit (output commit or clean termination).

The number of Ε windows between the opening Π Π and the closing Π is variable
and process-specific. The invariants are fixed:
- Starts with exactly Π Π
- Middle is all Ε (any deviation is a flag trigger)
- Ends with exactly one Π

### Type 2 — Settle Signal [Ε Ε Π] — Do Not Flag

A process that begins in equilibrium, stays in equilibrium, and exits cleanly.
This is a background service, a read-only query, a passive listener. It never
triggered the Π Π detection threshold. It is not flagged and not analysed further.
Ε Ε Π is the structural signature of a process that poses no cascade risk.

### Type 3 — Cascade Escalation [Π Π Π ...] — Observable and Terminal

```
Π Π Π Π Π Π Π
              ↑
         7th Π = TERMINAL
```

A process that cascades continuously without entering an equilibrium phase.
Each Π represents a sampling window in which the process exhibits non-returning,
accumulating behaviour. By the 7th consecutive Π the cascade is confirmed
terminal — the process has committed irreversibly to a behaviour pattern that
does not self-correct.

The 7th Π threshold is the ↓Π event: the cascade has completed in the
behavioural sense. Termination is the correct response.

**Why 7:** Six consecutive Π windows allow for legitimate burst behaviour —
compilation, compression, large file transfer, video rendering. These are
transient cascades with a natural Ε return. A 7th consecutive Π without any
equilibrium signal means the process has no self-correcting mechanism and is
not responding to resource pressure. This is the structural definition of
a runaway cascade.

---

## Flag Logic

### Π Π triggers reactive scan — not a flag, a signal

Π Π means: this process is initialising with cascade character. Interesting.
Analyse. Check against the local learned vocabulary. If the process is known-safe
on this machine, log and continue. If unknown, watch for the next window.

### Π Π Ε is not a flag

Π Π followed by Ε means the process initialised and entered equilibrium. This is
the correct functional pattern. Continue monitoring passively.

### Π Π Π is the first escalation flag

Three consecutive Π windows means the process did not enter equilibrium after
initialisation. Elevate monitoring frequency. This is the EARLY state.

### Π Π Π Π Π Π Π is terminal

Seven consecutive Π windows without equilibrium. CRITICAL state. Terminate.

### Π Π Ε [non-Ε] — deviation from equilibrium phase

A process in the expected equilibrium phase that produces a non-Ε signal has
broken its own pattern. This is the evasion signature — a process that initiated
correctly and then deviated from its expected equilibrium behaviour. This is
flagged because legitimate processes do not voluntarily break their equilibrium
phase without a structural reason. Malware that sleeps after injection and then
resumes cascade activity produces exactly this pattern.

---

## Recursive and Nested Arguments

Processes spawn subprocesses. Each subprocess has its own TSA sequence. The parent
process sequence is a function of its own behaviour plus the aggregate character
of its children.

**Nesting rule:**

A parent process that is Ε-phase but spawns a Π Π child inherits the child's
cascade signal for the duration of the child's cascade phase. The parent's
effective sequence becomes Β (boundary) — it is self-regulating in its own right
but has a cascade-character dependency running beneath it.

A parent process that spawns a Π Π Π child escalates to Π itself regardless of
its own behaviour — a process tree where a child is cascading uncontrollably is
a cascading parent by structural consequence.

**Recursive flag:**

If a Π Π Π child spawns further Π Π Π grandchildren, the cascade is recursive.
Recursive cascades receive the same terminal threshold as flat cascades — the 7th
Π window at any level of the process tree is terminal for that branch. The parent
is flagged for inspection but not terminated unless its own sequence reaches
the terminal threshold independently.

---

## Thermal Watchdog — Pre-Π Layer

Temperature is the earliest detectable signal of anomalous activity. It is
Ε-type by physics: under constant workload, CPU and GPU temperature
self-regulates within a stable thermal envelope. A machine running the same
processes day after day maintains a predictable temperature distribution.
Monotone temperature rise over 7 days without a corresponding increase in
known-safe Π Π processes is a boundary violation — the Ε thermal signal is
drifting toward its bifurcation constant without a legitimate cascade
explanation.

This is the canary layer. It runs independently of the reactive log scanner
and fires before any Π Π sequence appears in process logs. Something is
accumulating beneath the surface — a slow cryptominer, a persistent background
exfiltration process running below the Π Π detection threshold, or hardware
stress from a process that has learned to evade the sequence scanner by staying
just below the cascade threshold in each individual window while producing
sustained thermal load across days.

### Thermal Bifurcation Constant

```
TEMP_BIFURCATION = learned_baseline + TEMP_DRIFT_THRESHOLD
```

TEMP_DRIFT_THRESHOLD default: +3°C above the 7-day rolling mean under the
current season and workload class. Learned locally per machine. A gaming
machine runs hotter than an office machine — the baseline is machine-specific,
not a global value.

### 7-Day Rolling Window

The watchdog maintains a 7-day rolling temperature log sampled at 1-minute
intervals from hardware monitoring interfaces (ACPI, WMI, lm-sensors). It
computes:

- **7-day trend slope:** linear regression over the rolling window. A positive
  slope above SLOPE_BIFURCATION indicates monotone drift.
- **Workload adjustment:** if known-safe Π Π processes increased over the same
  period (compilation season, video rendering project), the temperature rise
  is workload-explained and does not trigger.
- **Unexplained drift:** positive slope with no corresponding increase in
  known-safe high-load processes.

### Trigger Condition

```
IF slope_7day > SLOPE_BIFURCATION
AND workload_delta < WORKLOAD_THRESHOLD
THEN → "INVESTIGATE NOW"
```

The alert is advisory, not terminal. It does not terminate processes. It
prompts the user to examine what is running and elevates the reactive log
scanner to maximum sensitivity — the Π Π detection threshold is temporarily
lowered so that borderline signals that would normally be ignored are evaluated.

### State Machine Integration

```
THERMAL WATCHDOG (continuous, low priority, 1-min sampling)
    │
    ├── temp stable or workload-explained ──► no action
    │
    └── monotone rise over 7 days, unexplained
            │
            ▼
        "INVESTIGATE NOW"
        + elevate reactive scanner sensitivity
        + log thermal drift event
        + prompt user review of running processes
```

The thermal watchdog is the structural equivalent of the bearing CSP's
temperature monitoring — in the bearing, temperature remained Ε throughout
every deployment run, confirming the self-regulating boundary was intact.
Here, a temperature boundary violation is the first signal that the
self-regulating boundary has been breached by something the process-level
scanner has not yet caught.

### Microbiological Parallel — Thermal Layer

Fever is the immune system's thermal watchdog. A sustained low-grade fever
over days without an identified infection source is a clinical flag — something
is activating the immune system that has not yet produced a localised symptom.
The thermal watchdog is the computational equivalent: sustained thermal drift
without an identified process source is an investigation prompt, not a
diagnosis.

| Immune system | Thermal watchdog |
|---|---|
| Low-grade fever (days) | 7-day monotone temperature drift |
| No localised infection found | No known-safe process explains load |
| Clinical flag: investigate | "INVESTIGATE NOW" alert |
| Elevated immune sensitivity | Lowered Π Π detection threshold |

---

## Detection Architecture

### No active polling

The scanner does not intercept system calls or hook into the kernel in real time.
It reads existing OS event logs (Windows Event Log, ETW traces, /proc filesystem
snapshots, auditd output) at sampling intervals. The logs already exist. The
scanner adds no overhead to the processes it monitors.

### Reactive triggering on Π Π

The log reader scans continuously at low priority for Π Π signatures. Everything
else is ignored. When Π Π is detected the scanner elevates attention to that
process and begins windowed evaluation. Between Π Π detections the scanner is
effectively idle.

**What constitutes a Π window in log data:**

| Signal | Π threshold |
|---|---|
| File write rate | Above baseline × WRITE_BIFURCATION per window |
| Unique API calls | New calls not seen in prior windows for this process |
| Entropy of written bytes | Above ENTROPY_BIFURCATION (consistent with encryption) |
| Outbound connection rate | Above baseline × NET_BIFURCATION per window |
| Registry write rate | Above baseline × REG_BIFURCATION per window |
| Memory allocation delta | Non-returning growth above MEM_BIFURCATION |

**What constitutes an Ε window:**

All of the above within their self-regulating bounds. No new API calls. No
entropy anomaly. No write rate elevation. The process is doing what it always
does on this machine.

### Sampling windows

Window length is configurable per process class. Default: 10 seconds (consistent
with CSP bearing snapshot interval). Short-lived processes (< 3 windows) are not
evaluated — insufficient data for structural classification.

---

## Per-Machine Local Learning

The scanner learns what is normal on the specific machine it runs on. It does not
import a global statistical model trained on other machines.

**What is learned locally:**

For each process name and process class observed over time, the scanner records:
- The expected opening sequence (always Π Π for initiating processes, Ε for
  background services)
- The distribution of equilibrium phase lengths
- The bifurcation constants for each signal on this machine under this workload

A process that is Π Π Π on a compilation machine is normal. The same sequence on
a machine that never compiles is a flag. The local baseline captures this distinction
automatically — a global model cannot.

**Learning protocol:**

Initial period (configurable, default 7 days): scanner observes and records without
flagging. Builds the local vocabulary of known-safe sequences per process.

After initial period: any process whose sequence deviates from its learned pattern
is elevated for inspection. New processes (never seen on this machine) trigger
immediate reactive scan from first window.

**The local vocabulary:**

```
process_name → {
    expected_open:    [Π Π] or [Ε] or [Ε Ε],
    equilibrium_len:  mean ± std (in windows),
    bifurcation_consts: {write, net, mem, entropy, reg} per process,
    known_safe:       True after N clean observations
}
```

Known-safe status is revocable — a process that has been safe for months but
produces a new Π Π Π sequence loses known-safe status and is re-evaluated.

---

## TSA State Machine

```
LOG STREAM
    │
    ▼
[Ε window] ──────────────────────────────► IGNORE
    │
[Π Π detected]
    │
    ▼
CHECK LOCAL VOCABULARY
    │
    ├── known-safe + expected pattern ──► LOG + CONTINUE
    │
    └── unknown or unexpected
            │
            ▼
        REACTIVE SCAN
            │
            ├── Π Π Ε (enters equilibrium) ──► MONITOR PASSIVELY
            │
            ├── Π Π Π (no equilibrium)
            │       │
            │       ├── Π⁴ Π⁵ Π⁶ ──► ESCALATE + ALERT
            │       │
            │       └── Π⁷ ──────► TERMINAL — TERMINATE PROCESS
            │
            ├── Π Π Ε [deviation] ──► FLAG — INSPECT
            │
            └── recursive child cascade ──► FLAG PARENT + EVALUATE TREE
```

---

## Cascade Thresholds

| State | Sequence | Action |
|---|---|---|
| IDLE | Ε* | No action |
| WATCH | Π Π | Reactive scan initiated |
| EARLY | Π Π Π | Elevated monitoring, alert log |
| CASCADE | Π⁴ – Π⁶ | Active alert, user notification |
| TERMINAL | Π⁷ | Process termination |
| EVASION FLAG | Π Π Ε [non-Ε] | Inspection flag, elevated monitoring |
| SETTLE | Ε Ε Π | No action, not flagged |
| RECURSIVE | Child Π⁷ | Branch termination, parent flagged |

---

## Structural Constants

All bifurcation constants are derived locally per machine per process class.
No global values. Defaults used during the initial learning period only:

| Constant | Default | Meaning |
|---|---|---|
| WRITE_BIFURCATION | 10× baseline | File write rate cascade threshold |
| NET_BIFURCATION | 5× baseline | Outbound connection rate threshold |
| MEM_BIFURCATION | 3× baseline | Non-returning memory growth threshold |
| ENTROPY_BIFURCATION | 0.85 | Byte entropy threshold (1.0 = random) |
| REG_BIFURCATION | 5× baseline | Registry write rate threshold |
| TERMINAL_COUNT | 7 | Consecutive Π windows before termination |
| LEARN_PERIOD | 7 days | Initial observation period before flagging |
| WINDOW_LENGTH | 10s | Sampling window duration (default) |
| TEMP_DRIFT_THRESHOLD | +3°C | Temperature rise above 7-day rolling mean |
| SLOPE_BIFURCATION | locally learned | Minimum 7-day trend slope triggering alert |
| WORKLOAD_THRESHOLD | locally learned | Max known-safe load increase before temp rise is explained |
| THERMAL_WINDOW | 7 days | Rolling window for thermal watchdog |
| THERMAL_SAMPLE | 1 min | Thermal sampling interval |

---

## Microbiological Parallel — Formal Statement

| Immune system | TSA scanner |
|---|---|
| Self-tolerance (learned per organism) | Local vocabulary (learned per machine) |
| Pattern recognition receptors | Π Π reactive trigger |
| Innate immune response (fast, generic) | Immediate reactive scan on unknown Π Π |
| Adaptive immune response (slow, specific) | Per-process learned bifurcation constants |
| Clonal expansion (cascade of immune response) | Escalating window frequency at Π³–Π⁶ |
| Apoptosis (programmed cell death) | Terminal at Π⁷ |
| Autoimmunity (false positive against self) | Mitigated by local learning period |
| Immunological memory | known-safe vocabulary, revocable |
| Cytokine storm (immune cascade failure) | Recursive child cascade → parent flag |

The parallel is not superficial. Both systems solve the same structural problem:
distinguish self-regulating behaviour from cascading behaviour in a complex
environment with partial information, react proportionally to cascade severity,
and learn locally rather than from a global model. The TSA algebra is the
formalisation of the same dynamical distinction that the immune system implements
biologically.

---

## Validation Protocol

**Unit test:** Inject synthetic log traces with known Π/Ε patterns. Confirm
terminal at Π⁷, flag at Π Π Ε deviation, no flag at Ε Ε Π.

**Known-malware test:** Run against archived execution logs of known ransomware,
RAT, and keylogger samples. Confirm cascade detection before encryption completion,
C2 establishment, or keylog exfiltration respectively.

**False positive test:** Run against known-clean intensive processes (compilation,
video encoding, backup). Confirm no terminal flag. Confirm Π Π Π may occur but
returns to Ε before Π⁷.

**Thermal watchdog test:** Simulate sustained background CPU load below the
Π Π detection threshold over 7 days. Confirm monotone temperature drift
triggers "INVESTIGATE NOW" before any process-level flag fires.

**Local learning test:** Run on two machines with different workload profiles.
Confirm that the same process produces different bifurcation constants on each
machine and that known-safe status is machine-specific.

---

## Relationship to CSP Framework

The TSA virus scanner is the CSP architecture applied to process behaviour rather
than bearing vibration. The structural mapping is exact:

| CSP (bearing) | TSA scanner (process) |
|---|---|
| RMS vibration | File write rate / memory delta |
| Kurtosis | API call entropy / novelty |
| Temperature (Ε throughout) | CPU/GPU thermal watchdog (7-day drift = INVESTIGATE NOW) |
| RMS_BIFURCATION | WRITE_BIFURCATION (locally learned) |
| HEALTHY → CRITICAL | IDLE → TERMINAL |
| Consecutive threshold confirmation | Π⁷ terminal count |
| Stratified per-bearing baseline | Per-process local vocabulary |
| Streaming 10s snapshots | Reactive windowed log scan |

The cascade detection lead time in the bearing CSP (17–68 minutes before failure)
has a direct analog here: the scanner detects the cascade at Π³ with 4 windows
remaining before terminal. At 10-second windows that is 40 seconds of lead time
before Π⁷ — sufficient for alert, user notification, and graceful process
suspension before forced termination.

---

*Working methodology — bifurcation constant calibration and false positive rate
pending validation against reference execution trace corpus.*
