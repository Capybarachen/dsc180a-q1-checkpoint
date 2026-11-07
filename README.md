# DSC 180 D32: Steering Diffusion Models — Q1 Checkpoint

This is code for my assignment 1 checkpoint. I use NVIDIA's pre-trained EDM model to generate CIFAR-10 pictures, and guide the generation using conditioning and classifier-free guidance (CFG) to control the generated content. I use label accuracy and FID to evaluate the results, and I also use CIFAR-10 and MNIST to train small CFG models.

## Files

| File | What it is |
|---|---|
| `cifar10_edm_lab.ipynb` | This is the CIFAR-10 EDM notebook provided by the course. I executed Parts 1–6 and completed the code for Part 3. |
| `mnist_cfg.ipynb` | My notebook use MNIST data to train the U-Net model provided by the course to support CFG, and evaluate the results. |
| `mnist_guidance_lab.py` | The course's MNIST helper code (U-Net, classifier, sampler), unchanged. |
| `figures/` | The figures in the report. |
| `NOTES.md` | My answers to part 3 and part 5 's questions. |

## Setup

Python 3.10 up  and an NVIDIA GPU
```
pip install torch torchvision numpy matplotlib
```

Where I ran each part:

| Part | Hardware |
|---|---|
| CIFAR-10 parts 1–5 | run on Google Colab T4 GPU |
| CIFAR-10 part 6 and MNIST | run on my pc NVIDIA RTX 4070 Ti Super GPU |
| Full EDM training run |  run on UCSD DSMLP GPU |

## Data downloads

- **CIFAR-10 and EDM:** The “Downloads” cell in `cifar10_edm_lab.ipynb` will download all the required files, including EDM code, pre-trained EDM models, CIFAR-10 images, the Inception network and reference statistics required to calculate FID, and the ResNet-56 classifier.
- **MNIST:** the first cell of `mnist_cfg.ipynb` downloads it with `torchvision.datasets.MNIST`.
- **`evaluator.pt`** (the course's frozen MNIST classifier): run the "Get the model weights" cell of the course's
  `guidance_mnist.ipynb`, then put the file next to `mnist_cfg.ipynb`.

## How to reproduce each figure and table

Open the notebook and choose Run All. Figures will appear in each output.

| Report | File | Made by |
|---|---|---|
| Figure 1 | `p1_uncond_samples.png` | `cifar10_edm_lab.ipynb`, part 1 |
| Figure 2 | `p1_trajectory_uncond.png` | `cifar10_edm_lab.ipynb`, part 1 ("Inside the sampler") |
| Figure 3 | `p2_cond_samples.png` | `cifar10_edm_lab.ipynb`, part 2 |
| Figure 4 | `p3_cfg_cat.png` | `cifar10_edm_lab.ipynb`, part 3 |
| Figures 5, 6 | `p3_trajectory_cat_w1.png`, `p3_trajectory_cat_w4.png` | `cifar10_edm_lab.ipynb`, part 3 ("Your turn" cell) |
| Table 2, Figure 7 | `p5_cfg_sweep.png` | `cifar10_edm_lab.ipynb`, part 5 (1,000 images per w) |
| Figure 8 | `p6_loss_fid.png` | `cifar10_edm_lab.ipynb`, part 6 |
| Figures 9, 10 | `p6_nearest_n100.png`, `p6_nearest_n1000.png` | `cifar10_edm_lab.ipynb`, part 6 |
| Figures 11, 12 | `p6_cfg_n100.png`, `p6_cfg_n1000.png` | `cifar10_edm_lab.ipynb`, part 6 |
| Table 3, Figure 13 | `mnist_samples.png` | `mnist_cfg.ipynb`, evaluation cell |
| Figure 14 | `full_run_loss_fid.png` | Full EDM training run (below) |

**Full EDM training run (Figure 14).** 
I executed the command displayed in the "Encouraged" section of the CIFAR-10 notebook on DSMLP and trained for about 22 hours. When the container stopped after 6 hours, I used --resume to continue training.


## Use of AI and My Contributions

- **From the course:** `cifar10_edm_lab.ipynb` (except my answers and the Part 3 trajectory cell), `mnist_guidance_lab.py`, and the FID functions copied into `mnist_cfg.ipynb`.

- **My work:**
  - Set up PyTorch with CUDA on my PC. I ran CIFAR-10 Parts 1–5 on Google Colab and Part 6 on my own GPU.
  - Wrote the data loading, training loop with label dropout and EMA, and evaluation loop in `mnist_cfg.ipynb` based on Claude’s suggestions. I then trained and evaluated the model and asked Claude to review the code.
  - Ran the optional full EDM training on DSMLP for about 22 hours, restarting it when the containers stopped.
  - Looked at the figures, saved them, and chose which ones to include in the report.
  - Answered the Part 3, Part 5, and “Before running” questions based on my understanding and observations.
  - Wrote the README, `NOTES.md`, and report, and set up the GitHub repository and Overleaf report.

- **Claude’s help:** Claude suggested the Part 3 trajectory code and helped me with the writing structure and grammar. It created the table under “How to reproduce each figure and table” in the README based on my keywords and helped with the LaTeX formatting. For the optional full EDM training, Claude wrote the scripts and helped me fix DSMLP errors.

