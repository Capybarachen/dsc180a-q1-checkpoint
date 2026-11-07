# Notes: Q1 checkpoint

Figures are in `figures/`. How each one was made is in the [README](README.md).
Tables and a sentence on each figure are in the report.

## Part 3: trajectories with a condition

Class: cat, same seed for both. Figures: `figures/p3_trajectory_cat_w1.png`, `figures/p3_trajectory_cat_w4.png`

**1. At which noise level does the class first show in D(x; σ)? Is it earlier with w = 4?**
When w = 1, the image is still blurry at σ ≈ 3.3, and I can see the cat at σ ≈ 1.1. When w = 4, the shape of a cat starts to appear around σ ≈ 8.4, and I can see the cat's face around σ ≈ 3.3. So the cat appears earlier with w = 4.

**2. From which noise level on does the image barely change?**
From about σ ≈ 0.3. For both w = 1 and w = 4, D(x; σ) at σ = 0.3, 0.06, and 0.002 looks the same.

**3. How do the w = 4 estimates differ from the w = 1 ones at low noise?**
Their difference is that the w = 4 images have vivid colors and darker backgrounds. One background is almost completely black. The cats also look more like cartoons and face forward more often. The w = 1 images have softer colors and look more natural.

## Part 5: CFG sweep, 1,000 images per w

**Which w would you choose, and what does each measure miss? Look at the images, not only the numbers.**

I would choose w = 1.5. Almost every picture shows the requested class (98.7%), FID = 31.44 is almost the same as at w = 0, and FID_class = 107.6 is the lowest.

What each measure misses: label accuracy only checks whether the classifier identifies the correct category and does not check the quality or diversity of the pictures. The accuracy rate at w = 4 is still 98.9%, but the pictures are oversaturated and look like cartoons. FID does not consider labels, so it cannot determine whether the picture matches the requested class. FID_class uses only 100 pictures per category, so the results are noisy, and the value is much higher than the overall FID.

These measures can't show that the pictures look like cartoons when w = 4. I can only see this from Figure 4 in the report.

## Next steps

- Choose an attribute to study and find a dataset with labels for it.
