# D3-Gym

**Note**: In this anonymous release, we do not include D3-Gym environments (i.e. docker environments with full pre-installed dependencies) and full model trajectories due to GitHub size limitations. These items will be shared on DockerHub and HuggingFace respectively as part of the official release. We do provide the lightweight metadata from all D3-Gym tasks in `tasks/` folder. 

D3-Gym is the first automatically constructed dataset of **verifiable environments** for **Data-Driven Discovery**. It contains 565 tasks derived from 239 real-world multi-disciplinary  scientific repositories.  

Each task includes:
- a natural language instruction,
- an executable environment with pre-installed dependencies,
- input datasets and artifact previews,
- a reference implementation,
- and an automatically generated evaluation script.

---

## Using D3-Gym Environments

All task environments are distributed as Docker images via `Redacted Link`.

Each image is a self-contained unit representing a single data-driven discovery task. It includes the task specification, datasets and previews, reference outputs, and evaluation script, along with pre-installed dependencies.

To solve a task, provide a `solution.py` that:
- reads the provided datasets, and  
- writes outputs to `pred_results/`.

The evaluation script compares your outputs against the reference and returns a pass/fail decision with a short explanation.

For easier browsing, we also provide an annotation sheet with metadata for all tasks on <a href="https://huggingface.co/datasets/osunlp/D3-Gym">HuggingFace</a>.  


---

## Quick Start

Pull a task image and inspect it:

~~~bash
docker pull owner/redacted_repo:task_1
docker run --rm owner/redacted_repo:task_1 inspect
~~~

Run your solution and evaluate:

~~~bash
docker run --rm \
  -v $(pwd)/solution.py:/task/solution.py:ro \
  owner/redacted_repo:task_1 run_and_eval
~~~

---

## Environment Structure

Each Docker image exposes the following directory layout:

~~~
/task/
  task_instruction.txt     # task description
  datasets/                # input data (CSV, JSON, images, etc.)
  *_preview.txt            # dataset schema previews
  eval_script.py           # evaluation logic
  gold_results/            # reference outputs
  pred_results/            # expected location for your outputs
  entrypoint.sh            # command routing
~~~

## Providing Your Solution or Outputs

~~~bash
# Run and evaluate a solution
docker run --rm \
  -v $(pwd)/solution.py:/task/solution.py:ro \
  owner/redacted_repo:task_151 run_and_eval

# Evaluate precomputed results
docker run --rm \
  -v $(pwd)/my_results:/task/pred_results:ro \
  owner/redacted_repo:task_151 eval

# Interactive debugging session
docker run --rm -it owner/redacted_repo:task_151 shell
~~~

---

## Downstream Use Cases

D3-Gym supports workflows that require executable environments with verifiable evaluation signals for data-driven discovery (e.g. reinforcement learning, self-improvement, etc.).

One use case is generating training trajectories (e.g., reasoning traces and solutions). The trajectories used in our experiments are available on `Redacted Link`. 

---

## Disclaimer

Repositories used in the creation of D3-Gym are under permissive licenses. We provide a full breakdown of licenses below. There are also 39 repositories that do not provide any license information; we assume these permit use for research purposes.

### License Distribution

| License                | Count |
|------------------------|-------|
| MIT                    | 99    |
| GNU (GPL, AGPL, LGPL)  | 43    |
| None                   | 39    |
| BSD                    | 29    |
| Apache                 | 22    |
| CC                     | 4     |
| ISC                    | 1     |
| Custom                 | 2     |
| **Total**              | **239** |

### Custom-Licensed Repositories
- BrainIAC  
- DeepDelta

---
