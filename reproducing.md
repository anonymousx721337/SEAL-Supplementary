---
layout: default
title: VaRA
---

## Reproducing the Results with VaRA

Our replication package already includes the results for our experiments. 
Here, we show how these results can be reproduced using VaRA.
Reproducing our results consists of two steps: (1) building VaRA, and (2) running the experiments using VaRA.

### Building VaRA

<blockquote style="color: #ff0000; border-left-color: #ff0000;">
   <p>
      <strong>Note for Reviewers:</strong>
      VaRA will be publicly available once this paper is published.
      Therefore, the automated installation of VaRA as described below will not work without proper access rights to its git repository.
      However, if you want to run VaRA yourself and need access to VaRA during your review, please contact us and we will gladly grant you access to VaRA.
   </p>
</blockquote>

1. First, we need to install the VaRA-Tool-Suite as shown for the [replication package]({{ "/index.html#replication-package" | relative_url }}) in steps 1-4.<br/>
   There are some additional dependencies to build vara and run all experiments:
   ```bash
   sudo apt install autoconf cmake ninja-build googletest libboost-all-dev libpapi-dev libsqlite3-dev libxml2-dev libcurl4-openssl-dev
   ```
2. The tool suite can clone and checkout all necessary repositories in the correct way with the following command:
   ```bash
   vara-buildsetup init vara
   ```
3. Finally, we can compile VaRA using this command:
   ```bash
   vara-buildsetup build vara
   ```
   Depending on your machine, this step may take a while.

For more information on how to build VaRA, we refer the reader to the [documentation](https://vara.readthedocs.io/en/vara-dev/vara-ts/vara-buildsetup.html)


### Running the experiments

1. First, we need to extract the replication package as shown in step 5 [here]({{ "/index.html#replication-package" | relative_url }}).
2. Our replication package already ships with the result files as we can see with the following command:
   ```bash
   vara-cs status --legend -s GenerateBlameReport
   ```
   ```
   CS: project_42: (Success / Total) processed [Success/Incomplete/Failed/CompileError/Missing/Blocked]

   CS: brotli_0:  (  1/1) processed [1/0/0/0/0/0]
   CS: curl_0:    (  1/1) processed [1/0/0/0/0/0]
   CS: grep_0:    (  1/1) processed [1/0/0/0/0/0]
   CS: gzip_0:    (  1/1) processed [1/0/0/0/0/0]
   CS: htop_0:    (  1/1) processed [1/0/0/0/0/0]
   CS: libpng_0:  (  1/1) processed [1/0/0/0/0/0]
   CS: libssh_0:  (  1/1) processed [1/0/0/0/0/0]
   CS: libtiff_0: (  1/1) processed [1/0/0/0/0/0]
   CS: lrzip_0:   (  1/1) processed [1/0/0/0/0/0]
   CS: lz4_0:     (  1/1) processed [1/0/0/0/0/0]
   CS: opus_0:    (  1/1) processed [1/0/0/0/0/0]
   CS: xz_0:      (  1/1) processed [1/0/0/0/0/0]
   --------------------------------------------------------------------------------
   Total:  ( 13/13) processed [13/0/0/0/0/0]
   ```
   Since we want to generate these files by ourselves, we need to delete the original result files.
   Should we need to recover the original files later on, we can simply unzip the replication again in the same location.
   ```bash
   vara-cs cleanup -exp GenerateBlameReport all
   ```
   We can confirm that all result files were deleted again with
   ```bash
   vara-cs status --legend -s GenerateBlameReport
   ```
   ```
   CS: project_42: (Success / Total) processed [Success/Incomplete/Failed/CompileError/Missing/Blocked]

   CS: brotli_0:  (  0/1) processed [0/0/0/0/1/0]
   CS: curl_0:    (  0/1) processed [0/0/0/0/1/0]
   CS: grep_0:    (  0/1) processed [0/0/0/0/1/0]
   CS: gzip_0:    (  0/1) processed [0/0/0/0/1/0]
   CS: htop_0:    (  0/1) processed [0/0/0/0/1/0]
   CS: libpng_0:  (  0/1) processed [0/0/0/0/1/0]
   CS: libssh_0:  (  0/1) processed [0/0/0/0/1/0]
   CS: libtiff_0: (  0/1) processed [0/0/0/0/1/0]
   CS: lrzip_0:   (  0/1) processed [0/0/0/0/1/0]
   CS: lz4_0:     (  0/1) processed [0/0/0/0/1/0]
   CS: opus_0:    (  0/1) processed [0/0/0/0/1/0]
   CS: xz_0:      (  0/1) processed [0/0/0/0/1/0]
   --------------------------------------------------------------------------------
   Total:  (  0/13) processed [0/0/0/0/13/0]
   ```
3. Running the experiments is now as simple as:
   ```bash
   vara-run -E GenerateBlameReport
   ```
   Or to run the experiment only for a single case study:
   ```bash
   vara-run -E GenerateBlameReport opus
   ```
4. Once the experiments are finished, we can confirm that the result files were correctly produced using the same `vara-cs status` command as in step 2 and also generate all the plots by executing `vara-art generate`.

> **Note:** Depending on the case study, VaRA can have very high resource requirements.
>           While smaller case studies can run on a modern desktop PC without issues, larger case studies may take 250GB of RAM or more and may take 20+h to complete depending on the CPU and other factors.
>           With some [additional setup](https://vara.readthedocs.io/en/vara-dev/vara-ts/slurm.html), the tool suite supports dispatching experiments to a slurm cluster.


> **Note** The reference system for our experiments is Debian 10, and they may or may not run on other systems because of incompatible library versions.
>          To remedy this issue, our experiments can also be executed inside an OCI compliant container.
>          Our [documentation](https://vara.readthedocs.io/en/vara-dev/tutorials/container_guide.html) gives a detailed description on how to set up the tool suite's container support.
>          This can also be combined with slurm.