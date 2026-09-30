# AURORA F1 — Data Source & Access Verification Report

**Project:** AURORA — Autonomous Upstream Reservoir Optimization and Risk-Aware Agent  
**Course:** SYSC 4907 — Fourth-Year Engineering Project  
**Document ID:** F1  
**Status:** CONDITIONAL PASS  
**Date:** 2026-09-22

---

## 1. Purpose

The purpose of this report is to determine whether the principal external
data and software resources required by AURORA exist, are accessible to the
team, and can be obtained from authoritative sources.

This report addresses the first feasibility question raised during the
initial supervisor discussion: whether the project depends on reservoir data
or external resources that may later prove inaccessible or unavailable.

F1 is deliberately limited to source existence, access, provenance, local
possession where appropriate, and basic artifact integrity.

F1 does **not** attempt to establish that every variable required by AURORA
is present or sufficient, that OPM Flow can successfully execute the selected
Egg cases, or that the Volve dataset contains every variable required for
real-field grounding. Those questions are addressed in later feasibility
documents.

---

## 2. AURORA External Resource Requirements

The current AURORA architecture depends on three principal external resources:

1. **The Egg Model** — a geological reservoir ensemble used as the principal
   controlled reservoir benchmark.

2. **OPM Flow** — the selected full-physics reservoir simulator used to
   generate high-fidelity reference trajectories and evaluate the effects of
   alternative reservoir-control actions.

3. **The Volve Field Dataset** — real petroleum-field data used for
   real-field grounding and reduced-order/CRM plausibility analysis.

The Carleton SYSC 4907 project information is also preserved as an
authoritative reference for capstone requirements.

---

## 3. Egg Model Dataset

### 3.1 Intended Role in AURORA

The Egg Model is intended to serve as AURORA's principal controlled
geological benchmark.

It provides the environment in which alternative reservoir-control actions
can ultimately be evaluated across multiple geological realizations.

AURORA does not treat the Egg Model as real field data. Its purpose is
controlled simulation and geological generalization testing.

### 3.2 Authoritative Source

The dataset was obtained from the TU Delft / 4TU Research Data distribution
associated with the Egg Model.

Persistent identifier:

https://doi.org/10.4121/uuid:916c86cd-3558-4672-829a-105c62985ab2

The associated publication is:

Jansen, J. D., Fonseca, R. M., Kahrobaei, S., Siraj, M. M.,
Van Essen, G. M., & Van den Hof, P. M. J. (2014).
*The Egg Model — A Geological Ensemble for Reservoir Simulation*.
Geoscience Data Journal.

A local copy of the publication is stored at:

`references/egg/Jansen_2014_The_Egg_Model.pdf`

### 3.3 Local Dataset Artifact

The original downloaded dataset has been preserved at:

`data/egg/egg_model_original.zip`

The archive has not been modified in place.

Recorded size:

`49,267,594 bytes`

Recorded SHA-256:

`ec7cecd344a31f9c3244078bb0e895b1a99c81a99603d4a6082d4c326c775434`

The complete provenance and checksum record is stored in:

`docs/feasibility/evidence/F1/source_manifest.txt`

### 3.4 Archive Integrity

The archive was tested using:

`unzip -t`

The integrity test completed with:

`No errors detected in compressed data of data/egg/egg_model_original.zip.`

The full integrity-test output is preserved in:

`docs/feasibility/evidence/F1/egg_zip_integrity.txt`

**Result: PASS**

### 3.5 Basic Content Verification

Without extracting or modifying the archive, its contents were inventoried
using `unzip -l`.

The archive contains 141 entries with a total uncompressed size of
173,580,102 bytes.

The archive contains directories and input material associated with several
reservoir-simulation environments, including:

- Eclipse
- MRST
- MoReS
- AD-GPRS

It also contains a dedicated:

`Permeability_Realizations/`

directory.

Files observed in the archive include, among others:

- `Egg_Model_ECL.DATA`
- `ACTIVE.INC`
- `COMPDAT.INC`
- `mDARCY.INC`
- `SCHEDULE_NEW.INC`
- `Fluid_Data.inc`
- `Geo_Data.inc`
- `Initial_Data.inc`
- `Phi.inc`
- `Well_Data.inc`
- permeability input files
- well-connection information
- simulation rate output

The archive also contains permeability-realization files numbered from
`PERM1_ECL.INC` through `PERM100_ECL.INC`.

The complete archive listing is preserved in:

`docs/feasibility/evidence/F1/egg_archive_listing.txt`

This establishes that the locally obtained artifact is not merely a paper or
description of the Egg Model. It contains machine-readable reservoir and
simulation material suitable for detailed technical inspection.

Detailed assessment of these files is intentionally deferred to F2.

### 3.6 Egg Access Verdict

**PASS**

The Egg Model dataset required for the planned AURORA feasibility work has
been physically obtained, preserved locally, fingerprinted, integrity-tested,
and shown to contain reservoir/simulator data and the expected additional
permeability-realization files.

This closes the narrow F1 question of whether the Egg resource is merely
theoretical or inaccessible.

It does not yet prove data sufficiency for the complete AURORA architecture.

---

## 4. OPM Flow

### 4.1 Intended Role in AURORA

OPM Flow is the selected full-physics reservoir simulator.

Within AURORA it is intended to provide:

- high-fidelity reservoir trajectories;
- counterfactual evaluation of alternative control actions;
- reduced-order/full-physics mismatch measurements;
- geological generalization experiments; and
- final full-physics verification of candidate control strategies.

OPM simulations are treated as high-fidelity simulation references within
the experimental framework. They are not described as literal real-world
ground truth.

### 4.2 Authoritative Source

Official project:

https://opm-project.org/

Official installation information:

https://opm-project.org/?page_id=36

A local OPM Flow reference manual has been preserved at:

`references/opm/OPM_Flow_Reference_Manual_2025-10.pdf`

Recorded size:

`20,899,782 bytes`

Recorded SHA-256:

`7050907724c049fb1690e5845e78e01fe6f86b5317b07e25691299d506036df1`

### 4.3 Current Verification State

Official OPM documentation is accessible and has been obtained.

However, F1 deliberately does not count documentation availability as proof
that AURORA can successfully execute the Egg Model using OPM Flow.

OPM installation, version capture, compatibility testing, baseline Egg
execution, modified-control execution, output extraction, and repeatability
testing will be performed in F3.

### 4.4 OPM Access Verdict

**CONDITIONAL PASS**

There is no identified access barrier preventing the project from proceeding
to an OPM execution test.

Actual executability remains an explicit feasibility condition and must be
demonstrated in F3.

---

## 5. Volve Field Dataset

### 5.1 Intended Role in AURORA

The Volve Field Dataset is intended to provide real-field grounding.

Its role is distinct from Egg + OPM.

Volve may be used to examine historical petroleum-field measurements,
evaluate the plausibility of the reduced-order modelling pipeline, and
support CRM-related real-data analysis.

AURORA will **not** claim that historical Volve data prove that an AURORA
controller would have improved historical Volve operations.

Historical data contain the consequences of actions that were actually
taken. They do not provide observed counterfactual outcomes for arbitrary
alternative actions that were never executed.

Therefore:

**Volve provides real-field grounding.**

**Egg + OPM provide controlled counterfactual controller evaluation.**

### 5.2 Authoritative Source

Provider:

**Equinor**

Official source:

https://www.equinor.com/energy/volve-data-sharing

The official Volve licence has been preserved locally at:

`references/volve/Equinor_Volve_Data_Licence.pdf`

Recorded size:

`250,211 bytes`

Recorded SHA-256:

`14672b51cf672f20207ba587af0260cb5e6fdff3d63bdbf11628f504d6c77873`

### 5.3 Current Dataset Status

The complete Volve dataset has intentionally **not** been downloaded during
F1.

This is not presently considered an access failure.

The complete dataset is large and broad, while AURORA requires only a
specific subset of information relevant to reservoir/well history and
reduced-order modelling.

F7 will identify the required variables, wells, time periods, and files
before the project obtains and audits the relevant Volve subset.

### 5.4 Volve Access Verdict

**CONDITIONAL PASS**

The authoritative source and licence have been identified and preserved.

The relevant AURORA-specific data subset remains to be obtained and audited
during F7.

---

## 6. Carleton SYSC 4907 Requirements

The official fourth-year project information-session document has been
preserved locally at:


Recorded size:

`793,535 bytes`

Recorded SHA-256:

`d7424618665142da82e7edc526a4bf91e6fa7646e3b9d590c0498fcb28bdf71e`

This document is maintained as an authoritative project reference when
evaluating AURORA's engineering scope, testing, documentation, planning,
individual contributions, and deliverables.

---

## 7. Reproducibility and Evidence Preservation

F1 does not rely solely on manually written statements.

The following machine-generated evidence has been preserved:

### Source Manifest

`docs/feasibility/evidence/F1/source_manifest.txt`

Contains:

- SHA-256 hashes;
- file sizes;
- local artifact paths; and
- recorded timestamps.

### Egg Archive Integrity Test

`docs/feasibility/evidence/F1/egg_zip_integrity.txt`

Contains the complete output of the ZIP integrity test.

### Egg Archive Listing

`docs/feasibility/evidence/F1/egg_archive_listing.txt`

Contains the complete unmodified archive inventory.

### Source Provenance

`docs/feasibility/evidence/F1/source_provenance.txt`

Records authoritative source locations and intended AURORA roles.

### Access Verification

`docs/feasibility/evidence/F1/access_verification.txt`

Records the current PASS/PENDING state of each major F1 resource.

Together, these artifacts allow the F1 conclusions to be independently
checked rather than relying only on narrative claims in this report.

---

## 8. Current Limitations

F1 establishes accessibility and provenance, not complete technical
suitability.

The following questions remain intentionally open:

1. Does the Egg dataset contain or permit derivation of every state,
   observation, action, constraint, and output required by AURORA?

2. Are the geological realizations structurally suitable for the proposed
   train/calibration/final-test methodology?

3. Can OPM Flow successfully execute the selected Egg deck?

4. Can AURORA alter a legitimate reservoir-control variable and observe a
   physically meaningful change in the resulting full-physics trajectory?

5. Can Python programmatically extract the required simulator outputs?

6. Does Volve contain a sufficiently complete subset of historical variables
   for the proposed real-field grounding work?

7. Are the resulting reservoir-engineering assumptions physically
   defensible?

These questions map directly to F2, F3, F4, F5, and F7 and must not be
silently treated as resolved by F1.

---

## 9. Risk Assessment

At the completion of F1, no evidence has been found showing that the
principal external resources required by AURORA are fundamentally
inaccessible.

The most important remaining resource-related risk is no longer simply
"Can we find reservoir data?"

It is now:

**"Does the accessible reservoir data contain the right information, and can
the selected simulation pipeline transform it into the controlled,
quantitatively measurable experiments required by AURORA?"**

That question is testable and is the purpose of the next feasibility stages.

---

## 10. F1 Decision

# CONDITIONAL PASS

AURORA passes the initial external-resource access gate subject to the
technical feasibility tests defined in subsequent reports.

Specifically:

- **Egg dataset access:** PASS
- **Egg artifact integrity:** PASS
- **Egg basic machine-readable content:** PASS
- **Egg detailed data sufficiency:** PENDING F2/F4
- **OPM documentation/access:** PASS
- **OPM executable compatibility with Egg:** PENDING F3
- **Volve authoritative source:** PASS
- **Volve licence acquisition:** PASS
- **Volve AURORA-specific subset suitability:** PENDING F7

No result obtained during F1 currently justifies abandoning or redesigning
AURORA.

However, F1 alone is insufficient to issue the project's final GO decision.

The next feasibility gate is:

**F2 — Egg Dataset Technical Audit**

F2 will determine what the downloaded Egg dataset actually contains and
whether its reservoir, geological, well, schedule, control, and output
information is suitable for the AURORA architecture.
