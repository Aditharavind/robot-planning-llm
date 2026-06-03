# Robot Planning LLM

LLM-based robotic reasoning and task decomposition framework for generating structured execution plans from natural-language commands.

---

## Overview

Robot Planning LLM is a domain-adapted language model designed for robotic task planning, instruction understanding, and structured reasoning.

The project investigates how instruction-tuned large language models can be adapted to transform high-level human commands into machine-readable execution plans suitable for robotic systems.

Rather than generating free-form responses, the model produces structured JSON outputs that explicitly represent task hierarchies, execution dependencies, conditional logic, and action policies.

The goal is to bridge the gap between natural language instructions and executable robot behavior through structured reasoning and task decomposition.

---

## Motivation

Modern robot systems require more than perception and control.

Robots must also:

* Understand human instructions
* Decompose complex tasks
* Resolve execution dependencies
* Handle conditional logic
* Generate interpretable plans

Large Language Models possess strong reasoning capabilities but are not naturally aligned with robotic execution frameworks.

This project explores adapting LLMs into a planning layer capable of producing structured robotic workflows.

---

## Architecture

```text
Natural Language Command
            │
            ▼
     Instruction LLM
            │
            ▼
  Structured Planning Layer
            │
            ▼
      JSON Task Graph
            │
            ▼
      Robot Execution
```

The model is fine-tuned to transform natural language commands into structured planning outputs suitable for downstream robot controllers, policy executors, or orchestration systems.

---

## Training Pipeline

### Base Model

* Qwen2.5-7B-Instruct

### Fine-Tuning Method

* LoRA (Low-Rank Adaptation)
* 4-bit Quantization
* Unsloth Training Framework
* Gradient Checkpointing
* Mixed Precision Training (BF16)

### Training Features

* Parameter-efficient adaptation
* Reduced VRAM requirements
* Long-context instruction tuning
* Structured output supervision
* High-throughput training pipeline

---

## Structured Output Format

The model is trained to generate machine-readable planning outputs.

Example:

```json
{
  "summary": "Pick and place operation",
  "subtasks": [
    {
      "step": 1,
      "policy": "navigate",
      "fragment": "move_to_object",
      "target": "red_cube",
      "reasoning": "Robot must reach the object before grasping.",
      "depends_on": [],
      "condition": null
    },
    {
      "step": 2,
      "policy": "grasp",
      "fragment": "pick_object",
      "target": "red_cube",
      "reasoning": "Object is within reach.",
      "depends_on": [1],
      "condition": null
    }
  ]
}
```

The structure captures:

* Task hierarchy
* Action sequencing
* Dependencies
* Execution constraints
* Reasoning traces
* Conditional branches

---

## Research Focus

This project explores several research questions:

* Can language models serve as robot planning modules?
* How effectively can LLMs learn structured task decomposition?
* Can reasoning chains be converted into executable task graphs?
* How should robotic plans be represented for downstream execution systems?
* What planning abstractions transfer best from language models to robots?

---

## Dataset Design

Training data consists of:

* Natural-language robot instructions
* Structured planning targets
* Multi-step execution workflows
* Dependency-aware task sequences
* Conditional execution logic

The model learns to map free-form human commands into deterministic planning representations.

---

## Key Capabilities

### Task Decomposition

Transforms complex instructions into manageable execution steps.

### Dependency Modeling

Captures prerequisite relationships between subtasks.

### Conditional Planning

Represents execution constraints and decision branches.

### Structured Outputs

Produces machine-readable plans rather than conversational responses.

### Robotics-Oriented Reasoning

Optimized for instruction understanding and execution planning workflows.

---

## Example Use Cases

* Mobile robot task planning
* Manipulation task decomposition
* Human-robot interaction systems
* Warehouse automation
* Service robotics
* Autonomous workflow generation
* Multi-agent orchestration

---

## Technologies

* Python
* PyTorch
* Transformers
* Unsloth
* PEFT / LoRA
* TRL
* Qwen2.5
* JSON-based Planning Representations

---

## Future Work

* Hierarchical planning trees
* Multi-agent task allocation
* Tool-use integration
* Planner-executor architectures
* Vision-language planning
* Grounded execution feedback
* Long-horizon robotic reasoning

---

## License

MIT License
