# Python code for open-pit mine scheduling problem using a sequential decomposition algorithm

Sequential decomposition algorithm (SD-CPIT) for the Constrained Pit Limit Problem (CPIT), applied to the eleven CPIT instances of the MineLib library. Each period is scheduled by one integer program, solved with Gurobi through Python-MIP; the blocks extracted are removed and the next period is solved.

## Repository structure

| Folder | Contents |
|---|---|
| `01_newman1` to `11_mclaughlin` | One folder per MineLib instance: notebook (executed, with outputs), block model (`.blocks`), precedences (`.prec`), schedule obtained (`<instance>_solution.csv`), 3D plot (`<instance>_plot.html`) and production chart (`<instance>_results.png`) |
| `schedule_validation` | Independent feasibility check of all the schedules against the official MineLib files (see below) |
| `Results_Summary.xlsx` | Summary of the results (Table 2 of the article) |

## Running the notebooks

1. Download the folder of the instance you want to run.
2. Open the notebook in Jupyter and run all the cells. The first cell installs the packages used in the article (Python-MIP 2.0.0, pandas, numpy, matplotlib, plotly).
3. The subproblems are solved with Gurobi when a licence is available; otherwise the code uses the open-source solvers HiGHS or CBC, distributed with Python-MIP.

The column `period` of `<instance>_solution.csv` gives the extraction period of each block (periods numbered from 0; empty = not extracted).

### Files of `11_mclaughlin`

Because of the file size limit of GitHub, some files of `mclaughlin` are compressed:

* `mclaughlin_blocks.zip` and `mclaughlin_solution.zip`: unzip them in the same folder.
* `mclaughlin_prec.7z.001` and `mclaughlin_prec.7z.002`: keep both parts in the same folder and extract the first one with 7-Zip (https://www.7-zip.org), which joins the parts and produces `mclaughlin.prec` (567 MB).

## Schedule validation

The notebook `schedule_validation/schedule_validation.ipynb` checks every schedule using only the official MineLib instance files (`.cpit` and `.prec`), without any data or code of the optimisation notebooks:

1. every block exists and is extracted at most once;
2. every extraction period lies within the planning horizon of the instance;
3. every precedence is respected;
4. the consumption of every resource respects the official limits in every period;
5. the NPV recomputed with the official objective coefficients and discount rate equals the value reported in the article.

The same procedure is applied to the CPIT solution files distributed by MineLib (`*_cpit_gmunoz120723.sol`), which validates the procedure itself. All eleven SD-CPIT schedules and all eleven MineLib solutions are feasible (`schedule_validation_sdcpit.csv` and `schedule_validation_minelib.csv`).

To run it again, unzip `schedule_validation/mclaughlin.zip` (official file `mclaughlin.cpit`) in the same folder and prepare the files of `11_mclaughlin` as described above. The `.prec` and `_solution.csv` files are read from the instance folders.

## Data

The instances are those of MineLib (Espinoza et al., 2013), available at https://minelib.org/v1/.

<!--
You also can try to run online by clicking on any notebook below to open it directly in Google Colab. It will be necessary to upload the datasets.

## MineLib Datasets 

- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/01_newman1/newman1.ipynb) newman1
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/02_zuck_small/zuck_small.ipynb) zuck_small
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/03_kd/kd.ipynb) kd
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/04_zuck_medium/zuck_medium.ipynb) zuck_medium
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/05_p4hd/p4hd.ipynb) p4hd
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/06_marvin/marvin.ipynb) marvin
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/07_w23/w23.ipynb) w23
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/08_zuck_large/zuck_large.ipynb) zuck_large
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/09_sm2/sm2.ipynb) sm2
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/10_mclaughlin_limit/mclaughlin_limit.ipynb) mclaughlin_limit
- [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/douglasmazzinghy/2026-MME/blob/main/11_mclaughlin/mclaughlin.ipynb) mclaughlin
-->
## Article

The article, including all details about the algorithm, was submitted to Mining, Metallurgy & Exploration SME’s journal (https://link.springer.com/journal/42461) in August 2026 and revised in October 2026.
