**Author:** Giuseppe Muschetta  
**University:** University of Pisa  
**Degree:** M.Sc. in Data Science & Business Informatics  
**Course:** Business Process Modeling  
**Academic year:** 2024–2025

# Formal Workflow Verification with BPMN & Petri Nets

**From business requirements to coordinated workflows with documented formal correctness.**

This project models and analyses a company's internship lifecycle through **BPMN collaboration diagrams, role-specific Petri nets and composed workflow systems**. It connects the responsibilities of a Supervisor, an Intern and a Project Leader, then investigates how an internship-extension policy changes their communication and synchronization.

Developed for the **Business Process Modeling course in the M.Sc. in Data Science & Business Informatics at the University of Pisa**, the work combines process abstraction, formal modelling and interpretation of structural and behavioural analysis results.

**Key result:** the saved WoPeD analyses report soundness for both the baseline and the extended composed workflow. The extension adds coordination steps while preserving the recorded soundness result; the analysis also documents the structural dependencies introduced by composition.

[Read the full technical report](Giuseppe_Muschetta_BPM_Report.pdf) · [Explore the baseline BPMN model](bpm_project.bpmn) · [Explore the extended BPMN model](bpm_project_variant.bpmn)

## Project at a glance

| Scope | Included in the project |
| :--- | :--- |
| Business collaboration | Three communicating participants: Supervisor, Intern and Project Leader |
| Process versions | Baseline internship lifecycle and an extension variant |
| BPMN models | Two editable collaboration diagrams |
| Petri-net models | Six role-specific nets and two composed workflow systems |
| Analysis evidence | Eighteen diagrams and qualitative-analysis screenshots |
| Documentation | Seventeen-page technical report |
| Modelling tools | Camunda Modeler and WoPeD |

## The business process

The baseline workflow follows the internship from the initial interview to the final employment decision.

| Participant | Responsibilities |
| :--- | :--- |
| **Supervisor** | Conduct the interview, assign the intern to a work group, receive the final evaluation and decide whether to offer a job contract |
| **Intern / Trainee** | Contact the project leader, receive activities and deadlines, perform the assigned work and submit reports |
| **Project Leader** | Match activities to the intern's competencies, communicate assignments and deadlines, evaluate reports and manage the remaining internship time |

The process includes competence-checking loops, repeated activity assignments, report evaluation, deadline signalling and final evaluation. **Nine message flows** connect the participants in the baseline BPMN collaboration.

![Baseline BPMN collaboration for the internship lifecycle](original_process_images/bpmn_project_image.png)

*The baseline BPMN model separates local responsibilities into three pools and makes their communication explicit. [Open the full-size diagram](original_process_images/bpmn_project_image.png).*

## From collaboration to formal models

The project develops three complementary views of the same business scenario:

1. **BPMN collaboration:** responsibilities, decisions, events and communication between participants.
2. **Individual workflow nets:** the local control flow of the Supervisor, Intern and Project Leader.
3. **Composed workflow system:** communication places and synchronization between the three participants, including their coordinated completion.

In the composed baseline net, a final synchronization transition requires all three participants to reach their respective completion places before producing the token in the common final place. This makes **global completion an explicit modelling decision**.

| Workflow net | Baseline: places / transitions / arcs | Extended variant: places / transitions / arcs |
| :--- | :---: | :---: |
| Supervisor | 6 / 6 / 12 | 9 / 10 / 20 |
| Intern | 11 / 11 / 22 | 14 / 15 / 30 |
| Project Leader | 20 / 22 / 44 | 24 / 28 / 56 |
| **Composed system** | **44 / 39 / 96** | **57 / 50 / 128** |

*Counts follow the net statistics recorded in the supplied WoPeD analysis captures.*

[View the composed baseline Petri net](original_process_images/petri_workflow_net_image.png) · [View the composed extended Petri net](variant_process_images/variant_petri_workflow_net.png)

## The extension variant: coordinating a restart

The variant introduces a new business decision: the Supervisor can **extend the internship** after receiving the final evaluation.

That decision requires a coordination protocol:

1. The Supervisor announces the extension to both the Intern and the Project Leader.
2. Both participants acknowledge their readiness to continue.
3. The composed Petri net synchronizes the Supervisor's continuation with both readiness acknowledgements.
4. The internship resumes through the work-group assignment step.

The restart transition in the composed variant requires **three input places simultaneously**: the Supervisor's continuation and the readiness of the other two participants. The extension policy is therefore represented by a concrete synchronization barrier.

The BPMN collaboration grows from **9 to 15 message flows**, while the composed net grows from **44 to 57 places** and from **39 to 50 transitions**.

![Extended BPMN collaboration with internship-extension messages and readiness acknowledgements](variant_process_images/bpm_project_variant_image.png)

*The variant makes the extension decision, notifications and readiness acknowledgements visible across all three pools. [Open the full-size diagram](variant_process_images/bpm_project_variant_image.png).*

## Formal analysis and its findings

The report and archived WoPeD captures examine both **behavioural correctness** and **structural properties** of the workflow nets.

Soundness comprises three requirements:

- **Option to complete:** every reachable marking has a path to the final marking.
- **Proper completion:** reaching the final place leaves no residual tokens elsewhere.
- **No dead tasks:** every transition can fire in at least one execution from the initial marking.

For workflow-net analysis, the standard characterization relates soundness to liveness and boundedness of the **short-circuited net**, obtained by adding a transition from the final place back to the initial place. [Formal background: Workflow Verification](https://www.vdaalst.com/publications/p98.pdf).

### Recorded results for the composed systems

| Analysis item | Baseline | Extended variant |
| :--- | :---: | :---: |
| Soundness | Passed | Passed |
| Source places / sink places | 1 / 1 | 1 / 1 |
| Initial marking | Valid | Valid |
| Unbounded places | 0 | 0 |
| Dead transitions | 0 | 0 |
| Non-live transitions in the reported analysis | 0 | 0 |
| Free-choice violation groups | 1 | 3 |
| PT-handles | 16 | 40 |
| TP-handles | 15 | 24 |

The individual role nets report soundness with no free-choice violations or PT/TP-handles. Their composition introduces structural dependencies: **the integrated models are sound according to the saved analysis, while remaining non-free-choice and not fully well-structured**.

This distinction is central to the project. It explains how communication and synchronization increase structural complexity and why the interpretation of behavioural guarantees matters alongside the shape of the model.

| Baseline composed-system analysis | Extended composed-system analysis |
| :---: | :---: |
| ![Saved WoPeD analysis of the baseline composed system](original_process_images/petri_workflow_net_analysis.png) | ![Saved WoPeD analysis of the extended composed system](variant_process_images/variant_petri_workflow_net_analysis.png) |

*The green soundness results and orange structural diagnostics are both retained in the evidence. The table above summarizes these archived analyses.*

The technical report also examines **S-component coverage** and **coverability graphs for the individual roles**, comparing the baseline and extended workflows.

## Skills demonstrated

| Competency | Evidence |
| :--- | :--- |
| Business process abstraction | Translating an internship scenario into explicit roles, tasks, decisions and communication |
| Formal modelling | Developing individual and composed workflow nets with explicit initial and final markings |
| Coordination design | Modelling message exchanges, global completion and synchronized restart |
| Process change analysis | Extending the lifecycle and comparing its effect on model structure and recorded correctness properties |
| Verification literacy | Interpreting soundness, boundedness, liveness, free-choice violations and PT/TP-handles |
| Technical communication | Editable models, visual evidence and a report connecting the business scenario to formal analysis |

## Repository guide

| Model | Baseline | Extended variant |
| :--- | :--- | :--- |
| BPMN collaboration | [`bpm_project.bpmn`](bpm_project.bpmn) | [`bpm_project_variant.bpmn`](bpm_project_variant.bpmn) |
| Supervisor Petri net | [`petri_supervisor.pnml`](petri_supervisor.pnml) | [`variant_petri_supervisor.pnml`](variant_petri_supervisor.pnml) |
| Intern Petri net | [`petri_intern.pnml`](petri_intern.pnml) | [`variant_petri_intern.pnml`](variant_petri_intern.pnml) |
| Project Leader Petri net | [`petri_project_leader.pnml`](petri_project_leader.pnml) | [`variant_petri_project_leader.pnml`](variant_petri_project_leader.pnml) |
| Composed workflow system | [`petri_workflow_system.pnml`](petri_workflow_system.pnml) | [`variant_petri_workflow_system.pnml`](variant_petri_workflow_system.pnml) |

- [`original_process_images/`](original_process_images/): baseline BPMN and Petri-net diagrams, plus analysis captures.
- [`variant_process_images/`](variant_process_images/): extended-process diagrams and analysis captures.
- [`Giuseppe_Muschetta_BPM_Report.pdf`](Giuseppe_Muschetta_BPM_Report.pdf): complete methodology, model comparisons, coverability graphs and interpretation of the findings.

The BPMN files were authored with **Camunda Modeler**; the PNML files and qualitative-analysis captures come from **WoPeD**. All models are included in editable form.

## License

Feel free to explore, adapt, and reuse these models and the accompanying report content for **academic or research purposes**. If you extend or modify the models, please credit the original work.
