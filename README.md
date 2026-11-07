# DSC 180 D32: Steering Diffusion Models — Q1 Checkpoint

Code for my Quarter 1 checkpoint (mentors: Yusu Wang and Qingsong Wang). I generate CIFAR-10 images with
NVIDIA's pretrained EDM models, steer them with conditioning and classifier-free guidance (CFG), and measure them
with label accuracy and FID. I also train small CFG networks on CIFAR-10 and MNIST.

## Files

| File | What it is |
|---|---|
| `cifar10_edm_lab.ipynb` | The course's CIFAR-10 EDM notebook, run end to end (parts 1–6). I filled in the part 3 cell. |
| `mnist_cfg.ipynb` | My notebook: trains the lab's U-Net as a CFG network on MNIST and evaluates it. |
| `mnist_guidance_lab.py` | The course's MNIST helper code (U-Net, classifier, sampler), unchanged. |
| `figures/` | The figures in the report. |
| `NOTES.md` | My answers to part 3's questions. |

## Setup

Python 3.10+ and an NVIDIA GPU.

```
pip install torch torchvision numpy matplotlib
```

Where I ran each part:

| Part | Hardware |
|---|---|
| CIFAR-10 parts 1–5 | Google Colab, T4 GPU |
| CIFAR-10 part 6 and MNIST | My PC, RTX 4070 Ti SUPER |
| Full EDM training run | UCSD DSMLP GPU |

## Data downloads

- **CIFAR-10 and EDM:** the "Downloads" cell of `cifar10_edm_lab.ipynb` downloads everything it needs (about
  720 MB): EDM's code, the pretrained EDM networks, the CIFAR-10 images, the Inception network and reference
  statistics for FID, and the ResNet-56 classifier.
- **MNIST:** the first cell of `mnist_cfg.ipynb` downloads it with `torchvision.datasets.MNIST`.
- **`evaluator.pt`** (the course's frozen MNIST classifier): run the "Get the model weights" cell of the course's
  `guidance_mnist.ipynb`, then put the file next to `mnist_cfg.ipynb`.

## How to reproduce each figure and table

Open the notebook and choose **Run All**. Figures were saved as screenshots of the notebook output.

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

**Full EDM training run (Figure 14).** I ran the command printed by the "Encouraged" section of the CIFAR-10
notebook on DSMLP:

```
torchrun --standalone --nproc_per_node=1 train.py --outdir=training-runs --data=<cifar10 zip> --cond=0 \
    --arch=ddpmpp --batch=512 --batch-gpu=64 --duration=10 --snap=10
```

DSMLP containers stop after 6 hours, so I restarted the run with `--resume` from the latest training state
(about 22 hours over 5 containers). FID was computed on 1,000 samples from each snapshot, as in the notebook.

