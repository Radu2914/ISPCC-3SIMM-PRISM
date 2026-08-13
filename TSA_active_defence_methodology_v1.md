# TSA Active Defence Pipeline — Methodology v1

## Purpose and Framing

A four-stage active defence system building on the TSA Cascade Virus Scanner.
The scanner detects. This pipeline responds. The response is graduated: locate,
verify, monitor, deceive. At no stage does the system announce its presence to
the attacker. The defence is structurally invisible — the attacker observes a
functioning channel returning plausible data until the channel becomes useless
and is abandoned.

The pipeline operates entirely locally. No external threat intelligence feed.
No cloud submission. No vendor dependency. The system's knowledge of what is
legitimate is derived from its own learned vocabulary, accumulated per machine
over time.

---

## Stage 1 — Thermal Probe (Pre-Π Detection)

**Trigger:** Monotone CPU/GPU temperature rise over 7-day rolling window without
a known-safe workload explanation.

**Action:** Elevate reactive scanner sensitivity. Initiate Stage 2 immediately.

**Structural character:** Ε-boundary violation. The thermal self-regulation
of the machine has been breached by an unidentified load. Something is running
that has not yet produced a Π Π process signature.

Full specification: TSA Cascade Virus Scanner Methodology v2, Thermal Watchdog
section.

---

## Stage 2 — Registry and Folder Verification

### Step 2a — Registry Scan

On thermal trigger or Π Π detection, scan the Windows Registry (or equivalent
OS persistence layer) for:

- Recently written keys not present in the local known-safe registry vocabulary
- Keys pointing to executable paths in non-standard locations
- Autorun, scheduled task, and service entries added since the last clean snapshot
- Keys with obfuscated or randomly generated names in standard persistence paths

The known-safe registry vocabulary is built during the learning period —
the same 7-day initial period used by the process scanner. Any key not in the
vocabulary and not attributable to a known installed application is a candidate
for Stage 2b.

### Step 2b — Folder Verification

For each candidate registry entry, resolve the associated executable path and
folder. Attempt verification against the local known-safe application catalogue:

```
VERIFY(path):
    IF path ∈ known_safe_locations → PASS (log and continue)
    IF path ∈ system_protected_locations → PASS (log and continue)
    IF path is signed by known-safe publisher AND signature valid → PASS
    IF none of the above → UNVERIFIABLE
```

**UNVERIFIABLE path action: delete immediately.**

No quarantine. No user prompt. No second opinion requested. An executable in
an unverifiable location that the antivirus cannot confirm as legitimate is
removed without delay. This is the innate immune response — unrecognised
structure is eliminated before it can establish further persistence.

The deletion is logged with full path, registry key, file hash, and timestamp.
The registry key pointing to the deleted path is also removed.

### Verification Catalogue

The known-safe application catalogue is maintained locally:

```
known_safe_locations = {
    standard_install_paths,        # Program Files, /usr/bin, /opt
    user_confirmed_paths,          # explicitly approved by user
    publisher_whitelist,           # verified code signing certificates
    OS_system_paths                # protected system directories
}
```

The catalogue is updated on application install and reviewed on major OS
updates. It is never imported from an external source — it is built from
what is actually installed on this machine.

---

## Stage 3 — Communication Marking

### Trigger

A process that passed folder verification (it exists and is partially
attributable) but exhibits suspicious behaviour — Π Π Π sequence, thermal
contribution, or registry anomaly — enters Stage 3.

The decision to proceed to Stage 3 rather than immediate deletion is made
when the process has enough legitimate attributes to make deletion ambiguous
but enough suspicious attributes to warrant surveillance.

### Marking Protocol

All inbound and outbound communication from the flagged process is marked
and logged:

```
PER PACKET LOG:
    timestamp
    source IP + port
    destination IP + port
    data volume (bytes)
    direction (in/out)
    protocol
    entropy of payload (high entropy = encrypted/compressed)
    timing interval to previous packet (regularity = C2 heartbeat)
```

The communication is not blocked. Blocking announces the defence. The
attacker observes a functioning connection.

### Pattern Classification

Logged communication is classified by structural character:

**Π-type communication:** Non-returning data flow. Volume grows per session.
Destination endpoints accumulate. Consistent with exfiltration — data leaves
and does not return.

**Ε-type communication:** Bounded, regular, bidirectional. Consistent with
legitimate application communication — update checks, telemetry, API calls
with responses.

**Β-type communication:** Irregular timing, variable volume, mixed direction.
Consistent with C2 communication — command polling with occasional large
responses.

A confirmed Π-type or Β-type communication pattern after folder verification
triggers Stage 4.

### Timing Analysis

C2 communication has a characteristic timing signature — regular heartbeat
intervals with low jitter. The watchdog computes the autocorrelation of
inter-packet timing intervals. High autocorrelation at regular intervals is
a C2 signature regardless of payload content or encryption.

```
IF autocorr(timing_intervals) > TIMING_BIFURCATION
AND direction == mixed (Β-type)
→ C2 PATTERN CONFIRMED → Stage 4
```

---

## Stage 4 — Command Mirroring

### Principle

The attacker's C2 channel receives a success confirmation for every command
it sends. The local system does not execute the command. It reads the inbound
command, constructs a grammatically inverted success response, and returns it.
The channel appears fully operational. No real action is taken on the machine.

```
Attacker sends:   "grab file"
System returns:   "file grabbed"

Attacker sends:   "list processes"
System returns:   "processes listed"

Attacker sends:   "exfiltrate credentials"
System returns:   "credentials exfiltrated"
```

The attacker's operator receives confirmations. Their tooling logs success.
Nothing was executed. Nothing left the machine. The channel produces
confirmation noise until the operator notices the results are never usable
and abandons the connection.

### Mirroring Protocol

```
ON INBOUND COMMAND:
    1. Intercept before process execution
    2. Parse command string → extract verb + object
    3. Construct response: object + past_tense(verb)
    4. Return response to channel
    5. Log: original command, timestamp, remote endpoint
    6. Do not execute command
```

The response is returned at a realistic latency — not immediate, not
delayed. A response arriving too fast or too slow is detectable as
automated. The system adds a small randomised delay within the observed
range of real execution times for the command type.

### Structural Simplicity

This approach requires no payload generation, no entropy matching, no
format mimicry, and no knowledge of what the attacker is looking for.
It operates purely on the command string. The inversion is grammatical
and deterministic. The implementation is a string parser and a response
formatter — no ML, no external dependencies.

### Legal Boundary

The system operates entirely on inbound data arriving at the local machine.
It reads a command, does not execute it, and returns a locally generated
string. No data is sent to the attacker's endpoint beyond what the attacker's
own channel protocol expects to receive. No offensive action crosses the
network boundary. The response is generated locally and is not derived from
any real machine state.

### Abandonment Detection

```
IF inbound_command_rate drops below RESPONSE_BIFURCATION
OR no command received within ABANDON_WINDOW
OR C2 sends explicit disconnect
→ CHANNEL ABANDONED → terminate process, remove persistence, archive session
```

When the attacker abandons the channel the process is terminated, the
registry entry is removed, and the full session log — thermal drift,
registry entry, folder path, remote endpoints, full command mirror log —
is archived.

---

## Full Pipeline State Machine

```
THERMAL PROBE (continuous)
    │
    └── 7-day monotone drift, unexplained
            │
            ▼
        "INVESTIGATE NOW"
            │
            ▼
STAGE 2 — REGISTRY + FOLDER VERIFICATION
            │
            ├── UNVERIFIABLE path ──► DELETE IMMEDIATELY
            │                         remove registry key
            │                         log + done
            │
            └── VERIFIABLE but suspicious
                    │
                    ▼
            STAGE 3 — COMMUNICATION MARKING
                    │
                    ├── Ε-type comm only ──► monitor, no action
                    │
                    └── Π-type or Β-type comm confirmed
                            │
                            ▼
                    STAGE 4 — FALSE DATA INJECTION
                            │
                            ├── ongoing ──► inject, monitor abandonment
                            │
                            └── abandoned ──► terminate, remove, archive
```

---

## Structural Constants

| Constant | Default | Meaning |
|---|---|---|
| TIMING_BIFURCATION | 0.85 autocorr | C2 heartbeat regularity threshold |
| RESPONSE_BIFURCATION | 20% of baseline | Response rate drop indicating abandonment |
| ABANDON_WINDOW | 48 hours | Window over which abandonment is assessed |
| ENTROPY_MATCH_TOLERANCE | ±0.05 | False payload must match original entropy within this range |
| DECOY_CREDENTIAL_FORMAT | locally derived | Format template from observed real credential structure |

---

## Properties

| Property | Status |
|---|---|
| Passive detection | ✓ Thermal probe and log scanning add no process overhead |
| Immediate removal of unverifiable paths | ✓ No quarantine delay |
| Invisible defence | ✓ Channel never blocked or reset |
| No offensive action | ✓ Response is a locally generated string, not derived from real machine state |
| No payload generation | ✓ Command mirroring requires only string parsing and grammatical inversion |
| No external dependency | ✓ Fully local vocabulary and catalogue |
| Per-machine specificity | ✓ All constants learned locally |
| Attacker abandonment as exit condition | ✓ Channel closes when it produces no value |

---

## Microbiological Parallel — Full Pipeline

| Immune stage | Defence pipeline stage |
|---|---|
| Fever (systemic alert) | Stage 1 — thermal drift |
| Innate response: destroy unrecognised | Stage 2 — delete unverifiable path |
| Adaptive response: mark and track | Stage 3 — communication marking |
| Decoy receptor binding: pathogen binds, finds nothing | Stage 4 — command mirroring |
| Pathogen abandons host (unsuccessful infection) | Attacker abandons channel |
| Memory cell formation | Session archive for future vocabulary update |

The fourth stage has a precise biological analog: decoy receptor binding.
The immune system presents receptor structures that a pathogen binds to
without gaining entry — the pathogen expends its attachment mechanism,
receives a surface-level response, and the interaction produces nothing
useful. Command mirroring is the computational equivalent: the attacker
sends a command, receives a confirmation, expends their operational
attention, and gains nothing. The channel consumes the attacker's time
and tooling until the absence of real results causes abandonment.

---

## Validation Protocol

**Stage 2 test:** Present known-malware persistence paths to the verifier.
Confirm immediate deletion. Present known-safe paths. Confirm pass.

**Stage 3 test:** Inject synthetic C2 communication (regular heartbeat,
mixed direction). Confirm timing autocorrelation detection above
TIMING_BIFURCATION.

**Stage 4 test:** Send a set of known C2 command strings to the mirroring
layer. Confirm each returns a grammatically inverted success response at
realistic latency. Confirm no command is executed on the local system.
Confirm the command log captures the original command and remote endpoint.

**Abandonment test:** After false data injection, simulate C2 operator
disengagement. Confirm ABANDON_WINDOW detection and clean process
termination.

---

## Relationship to CSP and TSA Framework

The four-stage pipeline maps directly onto the CSP operational states:

| CSP state | Defence pipeline state |
|---|---|
| HEALTHY | Normal operation, thermal probe running |
| EARLY | Thermal drift detected, Stage 2 initiated |
| CASCADE | Communication pattern confirmed, Stage 3 active |
| CRITICAL | False data injection active, Stage 4 running |
| TERMINAL | Attacker abandons, process terminated, persistence removed |

The structural logic is identical to the bearing CSP: detect the Ε-boundary
violation early (thermal drift), confirm the cascade (registry + communication
pattern), intervene before ↓Π (false data injection before full exfiltration
completes), and terminate cleanly when the cascade has been neutralised.

---

*Working methodology — false data injection implementation and abandonment
detection pending validation against controlled malware sandbox.*
