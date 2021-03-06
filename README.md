# Assemble Cycles simulations for Antares-IOWA project

1. Download [Cycles](https://github.com/PSUmodeling/Cycles/releases/)
2. Compile Cycles
3. Download [default operation files](https://psu.app.box.com/folder/112000862463). These operation files should be placed at `input/operations`
4. [NLDAS data](https://psu.app.box.com/folder/115212797598) should be placed at `input/weather`
5. SSURGO soils (checked to be at or below saturation) should be placed at `input/soils`. These files are labeled by gnatsgo mukey
6. Download the 4 'GenCrops' crop files from the 'Iowa' folder on box. These should be placed in the Cycles input folder. [GenCrops70RH, GenCrops45RH, GenCrops30RH, GenCrops0RH]
7. Grab the input file for the scripts [`IA_EFC_PSU_CGSB_20200622.csv`](https://psu.app.box.com/folder/115371308739)
   - Put in Cycles folder just above input folder (along with scripts)
8. `IA_genScen_ALD.py` creates operation files and multimode files. It is currently set up to read in `CLU_CT_00RH_NCC_NF_hnrr.csv`. The input file can be changed on line 44: ` data = open("CLU_CT_00RH_NCC_NF_hnrr.csv")`.
    - It is set up to run the default scenario and one other scenario for testing. If you want to create files for certain scenarios or all of the scenarios, lines 6-17 (as shown below) can be uncommented. The scenarios should match up with file names listed in the folder [https://antaresgroup.egnyte.com/app/index.do#storage/files/1/Shared/Client%20Shares/Tableau_BLD/CGSB_data/CGSB_clu](https://antaresgroup.egnyte.com/app/index.do#storage/files/1/Shared/Client%20Shares/Tableau_BLD/CGSB_data/CGSB_clu)

    ```Python
    scen_interest = ['CT_NCC_NF_00RH','NT_RYE_NPS_30RH'
                 #,'CT_NCC_NF_30RH','CT_NCC_NF_45RH','CT_NCC_NF_70RH'
                 #,'RT_NCC_NF_00RH','RT_NCC_NF_30RH','RT_NCC_NF_45RH','RT_NCC_NF_70RH'
                 #,'NT_NCC_NF_00RH','NT_NCC_NF_30RH','NT_NCC_NF_45RH','NT_NCC_NF_70RH'
                 #,'CT_NCC_NPS_00RH','CT_NCC_NPS_30RH','CT_NCC_NPS_45RH','CT_NCC_NPS_70RH'
                 #,'RT_NCC_NPS_00RH','RT_NCC_NPS_30RH','RT_NCC_NPS_45RH','RT_NCC_NPS_70RH'
                 #,'NT_NCC_NPS_00RH','NT_NCC_NPS_30RH','NT_NCC_NPS_45RH','NT_NCC_NPS_70RH'
                 #,'CT_RYE_NF_00RH','CT_RYE_NF_30RH','CT_RYE_NF_45RH','CT_RYE_NF_70RH'
                 #,'RT_RYE_NF_00RH','RT_RYE_NF_30RH','RT_RYE_NF_45RH','RT_RYE_NF_70RH'
                 #,'NT_RYE_NF_00RH','NT_RYE_NF_30RH','NT_RYE_NF_45RH','NT_RYE_NF_70RH'
                 #,'CT_RYE_NPS_00RH','CT_RYE_NPS_30RH','CT_RYE_NPS_45RH','CT_RYE_NPS_70RH'
                 #,'RT_RYE_NPS_00RH','RT_RYE_NPS_30RH','RT_RYE_NPS_45RH','RT_RYE_NPS_70RH'
                 #,'NT_RYE_NPS_00RH','NT_RYE_NPS_30RH','NT_RYE_NPS_45RH','NT_RYE_NPS_70RH'
                 ]
    ```
9. Run `IA_genScen_ald.py`
10. Run all the 'CT_NCC_NF_00RH' scenarios in Cycles with spin-up first (`Cycles -s`). These scenarios (IOWA project has four[C,CS,CCS,S]) takes files in the soil folder, simulates from 1980-2016, and generates the spun-up soils.
11. Run others scenarios without spin-up. The other scenarios read in the spun-up soil files (`*_ss`) from the 'CT_NCC_NF_00RH' scenario, running from 2013-2016 (lines 44-45 in `IA_genScen_ald.py`).
12. Cycles output can be appended to the `CLU_CT_00RH_NCC_NF_hnrr.csv` file by running `scenOutput.py`.
    - This script reads in the `EFC/Antares` files, but you will need to tell it which one to read in. That is found on line 3 `ald_fname = 'CLU_CT_00RH_NCC_NF_hnrr.csv'`.
    - The 'CT_NCC_NF_00RH' is just the reference case, with no actual corresponding EFC .csv file. This business-as-usual scenario needs to be run regardless, and the `.csv` output is only for reference purposes. The other scenarios do have corresponding EFC `.csvs`

## How to handle common problems/errors
- If you need to replace/edit a crop file, you will need to redo Step 8 by re-running `IA_genScen_ald.py`





